---
layout: page
title:  "OSCP Journey"
date:   2016-04-08 
categories: 
---
I am an Information Security enthusiast, easily intrigued by things which I don't understand.
I have less than a year of working experience (as of July, 2016) and zero Penetration-Testing/Vulnerability Assessment experience.
I stumbled across <a href="https://www.vulnhub.com/">Vulnhub </a>one day and looking at the walkthroughs of various VMs submitted by different people, I was amazed by it.

I wanted to be able to do that, having a practical skill-set which can be validated.

I went on researching about courses/certifications which can help me in achieving my goals. I looked through various courses and its entity such as GIAC SANS, EC-Council CEH, SecurityTube, eLearningSecurity, and <a href="https://www.offensive-security.com/">Offensive Security</a>.
I then decided on <a href="https://www.offensive-security.com/information-security-training/penetration-testing-training-kali-linux/">Offensive Security's OSCP PWK</a> course.
Given it's pricing and what I'll get in return,(Videos, PDF, Certification attempt, and 3 months of VPN Lab access) I felt that it was extremely worth it as compared to the others.

I was quite hesitant at first as Offensive Security recommends the pre-requisite of having solid understanding of networking and reasonable Linux skills.
However, I believed that my determination and passion will outweigh all the pre-requisite.
With that, I signed up for 90 days PWK course. [Started on 10th April, 2016]
<p style="text-align:center;"><strong>- The 90 Days Journey -</strong></p>
The first month was basically going through the PWK materials, finishing the videos and going through the PDF. There were various exercises after each topic to challenge yourself, and I did not managed to complete some of them :(
I quickly jumped into the lab environment and started putting what I've learned into use. It was quite overwhelming especially when your enumeration scans return a ton of output, hahah.
I got stuck quite often, not knowing what I should do, and how. I came up with an attack plan which helped me quite a lot.

1. Do all possible enumeration (Port scan, version scan, OS scan, etc)
2. Try to figure out the purpose of the system (Web server, Mail server, end user, whatever)
3. Research on all the ports discovered and it's service running behind it (Google-Fu)
4. Find the most possible attack vector!

With that, I managed to progress myself through well. From single digit of hosts compromised to double.

The second month was fun and thrilling, I was basically on THE roll. Hacking through system after system, it was a great feeling.
I discovered various other networks which can only be accessed via certain hosts that were double homed.
I learned different privilege escalation routes that were not taught in the videos/pdf.
It was definitely more than launching a <a href="https://www.kernel-exploits.com/">pre-compiled kernel exploit</a>.

The third month was pretty much relaxing and chill. I did not do as much as the previous 2 months due to some personal reasons.

In the end, I was able to compromise the infamous top 3 machines. I did not really "pivot" into other network, which I felt that it was quite a waste as I could have learned more about port-forwarding.
<p style="text-align:center;"><strong>- The Exam -</strong></p>
I took my first certification challenge on 7th June, 2016. I was extremely close to passing, all I needed was a privilege escalation and I would have gotten it.
In the end I found out that it was an extremely silly mistake on my end, I already had the correct vector for it. F*CK!
(I found out after I passed the exam on my second attempt, and was exposed to a new section in the forums which contains brief information about the exam machines)
I took my second certification challenge on 30th June, 2016. My 23 days of waiting consists of:

- 9 days break
- Going through <a href="https://www.amazon.com/Hacker-Playbook-Practical-Penetration-Testing/dp/1512214566">The Hacker Playbook 2</a> (GOOD STUFF)
- Hacking the latest Vulnhub's VM (First page)
- Improving my enumeration game (Basically reading about everything pen-testing related)

The exam went well. I managed to secure enough points to pass after around 15-16 hours, and decided to work on my report straight. Everything fresh off my mind!
I completed whatever that was necessary for the submission on roughly the 18-19th hour into the exam, before going to bed.

2 days later I received the confirmation email from Offensive Security that I have passed my Certification challenge and is officially OSCP!
Best feeling ever.

<img class="alignnone size-full wp-image-784" src="https://scriptkidd1e.files.wordpress.com/2016/04/capture.jpg" alt="Capture" width="710" height="138" />
<p style="text-align:center;"><strong>- The Conclusion -</strong></p>
In my opinion, there is no "pre-requisite" to learning. Sure, you will be much better off and things will be easier if you had the prior experience, so what?
I will beat it with hard-work.

The only "pre-requisite" I feel is Time.

Time is extremely important for you to succeed in this course if you have little to no experience. There was a lot of self-researching to do.

True to the "rumours", the materials provided alone are DEFINITELY NOT ENOUGH to pass the OSCP exam.

For the past 3 months, my off days are literally non-existent. I spent 8-10 hours on my off days to read up on whatever I am lacking.
Sometimes even on my work days, I will sneak out some time for OSCP. Hehe.

3 months ago my practical skills are shit. 3 months later after the OSCP PWK course, I am quite confident that I can complete most of the Vulnhub's VMs without any walkthrough or reference.

What about real life penetration testing? I will find out when I land myself a Penetration Testing related job!

I will not post any reference that I've used, since the other 1337 OSCP reviews contain them all.

Word of advice - The references are pretty much useless if you have no idea what you're looking for, or how can the results be useful to you.

Understanding the PURPOSE of the things you do will bring you far!
Know what are you looking for, know what is useful for the situation.
(Gaining access or privilege escalation)

Thats about all,

Stay safe!