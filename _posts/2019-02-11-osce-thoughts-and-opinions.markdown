---
layout: post
title:  "OSCE Thoughts and Opinions"
date:   2019-02-11
categories: progress work
---
Happy belated Chinese New Year!

So... It has been 3 years since I took my OSCP from Offensive Security and back then, it was really a hell of a ride. After getting my OSCP, I was fortunate enough to be given an opportunity to do penetration testing stuff then.

I decided to give OSCE a go since I am kinda unfamiliar with the low level stuff like assembly, shellcoding, and debugging.

For those unaware, the OSCE's Overview and Syllabus are as follows:

>Course Overview & Syllabus
>Like other Offensive Security courses, CTP combines traditional course materials teaching advanced penetration testing skills with hands-on, practice within a virtual lab environment.  The course covers the following topics in detail.  View the full syllabus.

>Introduction  
>The Web Application Angle  
>Cross Site Scripting Attacks – Scenario #1  
>Real World Scenario  
>Directory traversal – Scenario #2  
>Real World Scenario  
>The Backdoor angle  
>Backdooring PE files under Windows Vista  
>Advanced Exploitation Techniques  
>MS07-017 – Dealing with Vista  
>Cracking the Egghunter  
>The 0Day angle  
>Windows TFTP Server – Case study #1  
>HP Openview NNM – Case study #2  
>The Networking Angle – Attacking the Infrastructure  
>Bypassing Cisco Access Lists using Spoofed SNMP Requests  
>GRE Route-Map Kung Fu  
>Sniffing Remote Traffic via GRE tunnel  
>Compromised Router Config  

Personally, the Web Application portion was really straight-forward as I have tons of experience doing that from work. The backdooring PE file was to me, the most fun chapter of the course.

OSCE as compared to OSCP, was more compact and dedicated. The materials are sufficient to pass the exams, but you must have a thorough understanding of it. It is quite difficult to fail if you understand the materials.

Below are my personal "pros" and "cons" of the course:

```
Pros:

- Exploitation of vulnerabilities. This will help to demonstrate impact.
- Better understanding of ASM, shellcode, debugging.
- Walkthroughs of classic exploitation techniques

Cons:

- It is a pain in the ass to have to RDP into the Windows boxes provided. I ended up setting my own instances of Windows to go through the materials
- Methods and techniques are dated. This is up to how you see it. Having a better grasp of the underlying concept is good. 
```

Overall I would say it is worth the effort and time. Thankfully my employer paid for it. A month of lab is more than enough to complete everything.

Some tips for the exam:


- Learning how to use a debugger is more important than understanding assembly. Many times you will need to set breakpoints at various locations to find out what is going wrong. 
- Take small steps. Be very cautious and make sure everything works as intended before advancing to the next step. This will save a lot of time.
- The HP Openview NNM was discussed during DefCon16, by none other than the author Mati himself:
<iframe width="560" height="315" src="https://www.youtube.com/embed/gHISpAZiAm0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
- A sample report is available from Offensive Security themselves. The reporting basically became a "fill in the blanks" portion.
https://support.offensive-security.com/osce-faq/#how-do-i-schedule-my-certification-exam
- Do your report while you attempt the exams! Saves a lot of time. I basically completed everything and the report as well in like ++~10 hours

That's it! First certificate of the year!
<div style="text-align: center"><img src="/images/offsec-osce-email.PNG" height="220" width="660"/></div>
