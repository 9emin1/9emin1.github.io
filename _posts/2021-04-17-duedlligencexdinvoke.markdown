---
layout: post
title:  "DueDLLigence x D/Invoke"
date:   2021-04-17
categories: progress work
---
Last year while looking at open source resources to come up with a payload dropper that is undetectable I came across an awesome project by FireEye, titled DueDLLigence:

> * https://github.com/fireeye/DueDLLigence

Quoting from their README it describes the project as follows:

>Shellcode runner framework for application whitelisting bypasses and DLL side-loading. The shellcode included in this project spawns calc.exe.

Pretty cool eh? I was able to come up with a dropper that went undetected by modern Windows Defender, leveraging on the CreateRemoteThread template given in the project without much modifications. Worked like a charm and it was great!

Basically the project uses the Unmanaged Export NuGet package by Robert Giesecke (https://www.nuget.org/packages/UnmanagedExports) to export functions that an executable will be looking for. For example, msiexec /y looks for DLLRegisterServer and the /z flag looks for DLLUnregisterServer. The project also uses P/Invoke to import unmanaged code from kernel32.dll for all the typical process injection requirements.

It was fun while it lasted, fortunately enough to last me through a Red Team gig. Looking at it again this year it appears that Windows Defender is now able to pick up the .DLL as TurtleLoader (lol) even when there was no shellcode in it (lol x 2). 

An attempt was made to clean out all unnecessary code, such as other imports/exports, and as well as renaming all the obvious variable names. Submitting the empty shellcode .DLL generated thereafter resulted in detection once again:

<div style="text-align: center"><img src="/images/dd.png" height="260" width="680"/></div>
<div style="text-align: center"><img src="/images/dd2.png" height="260" width="680"/></div>


The most surprising detection was the ability to identify it as DueDLLigence template.

The goal here was to at least have a working payload that bypasses Windows Defender minimally. Having a payload that works prepared on hand is always good instead of having to come up with one when a project has already started.

Knowing that the payload was able flagged without any shellcode in it it can only means that static analysis is picking it up. One of the possibility could be the imported calls were obvious to process injection techniques and the usage of P/Invoke leaves traces of the imported functions in the Import Address Table of the binary. I decided to look into alternatives to import unmanaged code and came across D/Invoke, shared by The Wover and Ruben Boonen. 

The following resources were of great help to understand the differences and integration into your existing C# tools:

> * https://thewover.github.io

> * https://youtu.be/FuxpMXTgV9s

After integrating and replacing P/Invoke imports with D/Invoke, the DueDLLigence template works like a charm again ;)

CreateThread shellcode launcher with meterpreter payload, bypassing Windows Defender:

<div style="text-align: center"><img src="/images/dd3.png" height="260" width="680"/></div>

It is good to see that detection has evolved from signature-based to more of technique-based and this can be more time consuming for bypasses.
