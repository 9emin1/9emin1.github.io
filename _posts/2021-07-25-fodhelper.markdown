---
layout: post
title:  "UAC Bypass? Fodhelper.exe? 2017?"
date:   2021-07-25
categories: progress work
---
UAC Bypass is very important especially in modern phishing compromises, whereby the user shell you receive will probably be an administrator privileged user account, but the context of the shell will not be of High integrity. This means that if you were to peform an elevated action, such as adding of a new local administrator account, or performing process dumping, it will not work. The default UID 500 Administrator account that has no UAC restriction is no longer active in default Windows 10 installation and you will have to create a new 'administrator' user account that has UAC restriction. 

It was great having a working UAC bypass on hand, allowing me to quickly elevated to a High integrity context (SYSTEM). This is required to peform credentials harvesting which is an essential step for lateral movement and moving forward in an engagement. I have been using the fodhelper module in the project SharpBypassUAC for UAC bypass as it allows execute-assembly which is really handy:

> * https://github.com/FatRodzianko/SharpBypassUAC

Unfortunately, Windows Defender started flagging it :( Let's investigate how it is being triggered and if it is possible to make fodhelper great again!

From the FodHelper.cs source code, we can see how the UAC bypass is implemented. It creates a new registry hive (under HKCU) "ms-settings\Shell\Open\command" with a hardcoded value of "DelegateExecute" and the command we want to execute in a High integrity context. 

```
            //Convert encoded command to a string
            string command = Encoding.UTF8.GetString(encodedCommand);

            //Set the registry key for fodhelper
            RegistryKey newkey = Registry.CurrentUser.OpenSubKey(@"Software\Classes\", true);
            newkey.CreateSubKey(@"ms-settings\Shell\Open\command");

            RegistryKey fod = Registry.CurrentUser.OpenSubKey(@"Software\Classes\ms-settings\Shell\Open\command", true);
            fod.SetValue("DelegateExecute", "");
            fod.SetValue("", @command);
            fod.Close();
```

It then executes the fodhelper.exe binary. The fodhelper.exe will go through the created registry hive and eventually executes the command we set as the value in registry item we created. 

```
            //start fodhelper
            Process p = new Process();
            p.StartInfo.WindowStyle = ProcessWindowStyle.Hidden;
            p.StartInfo.FileName = "C:\\windows\\system32\\fodhelper.exe";
            p.Start();
```

It then sleeps for 10 seconds and subsequently, removes the created registry as post activity cleanup. Neat.

We know that we were able to compile the binary successfully without triggering Windows Defender. The Windows Defender alert should be pretty clear as well that it is triggered from runtime and not due to static signature detection. We can further validate this as it can be observed that the registry values were created succesfully, and the registry will then be removed after that. The process that is spawned via the fodhelper.exe (the command we set) will be immediately terminated. It is worth noting that the commands will still get executed, so it could be useful for activities such as adding of a local administrator user, changing the default administrator password and making the account active, etc (end user will still receive the Windows Defender alert though!). Using it to launch an elevated shell session however will not work as it will get terminated immediately. 

SharpBypassUAC with fodhelper, executing notepad.exe. Notepad.exe did get executed and was terminated immediately, triggering the following Windows Defender alert:
<div style="text-align: center"><img src="/images/fb1.png" height="260" width="680"/></div>

Now we have a clearer understanding of the detection mechanism behind, we should be able to come up with a bypass. We verified that only the full flow of 1. registry creation + 2. execution/start of the fodhelper.exe process triggers Windows Defender. The registry creation/deletion alone does not. 

SharpBypassUAC without executing fodhelper.exe. No triggers and registry was created:
<div style="text-align: center"><img src="/images/fb2.png" height="260" width="680"/></div>

Lets try something raw and native using the same cmd.exe process. We executed REG ADD to create the necessary registry keys and values for fodhelper.exe. We then execute fodhelper.exe, launching notepad.exe. Nothing malicious but it triggers Defender as shown below:
<div style="text-align: center"><img src="/images/fb3.png" height="260" width="680"/></div>

Wow? So what was the trigger point?

As funny as it sounds.. Here is how we can bypass Windows Defender triggering on this UAC shit. We have to overwrite the registry key values we created before calling fodhelper.exe.. Yes.. just overwrite it with the same values, then call fodhelper.exe. So instead of: 

1. Create registry 
2. fodhelper.exe 
3. cleanup, 

we will have to do 

1. Create registry
2. Overwrite created registry
3. fodhelper.exe
4. cleanup

Here it goes...

<div style="text-align: center"><img src="/images/fbd.gif" height="260" width="680"/></div>

As shown above, we successfully executed notepad.exe in a High integrity context, using fodhelper.exe to bypass UAC. Windows Defender didnt trigger and we can see that notepad.exe didn't get terminated :)




