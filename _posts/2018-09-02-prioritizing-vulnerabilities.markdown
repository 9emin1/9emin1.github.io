---
layout: post
title:  "Prioritizing Vulnerabilities"
date:   2018-09-02 
categories: work
---
>I got 99 problems but XSS ain't one

One of the very importance aspect when performing technical delivery is the ability to prioritize vulnerabilities. For example... 

Looking through a report there are only a few (god bless) vulnerabilities being raised and so, which ones should be prioritized? (Obviously the critical ones, duh!)

Sometimes, it is not as straight-forward as it may seems. Fixing a vulnerability might not be as simple as removing a few lines of code, or adding a few lines of code. It may be from a library, a third-party code, or fixing the vulnerability might require a lot of time and effort, because possibly restructuring of the application core code base is required.

Apart from just looking at the severity of the identified vulnerabilities, what else can you look for?

Another important factor to look at is how easy can the vulnerability be exploited. This refers to:
- Can the vulnerability easily be spotted?
- Is it intuitive? Can it easily be 'accidentally' discovered?
- The success rate. To abuse (exploit) the vulnerability, does it require user-interaction? Any specific prerequisite?

It is important to <b>understand exactly how can the vulnerability be exploited</b>. This means that your Penetration Tester has to be technically capable enough to explain to you, step-by-step, on how to reproduce the vulnerability, and also provide a clear proof of concept on the <b>exploitation</b> of the vulnerability. 

Sounds hard? Let me give you an example.

Hackerman found an XSS on your application! Awesome. He immediately raise it as a Critical/High severity finding because...(?)

Yes Cross-Site Scripting (XSS) vulnerabilities can be severe and it is actually possible to exploit XSS to compromise all: Confidentiality, Integrity and Availability of the target. But usually this requires complexity, and is not a easy feat to pull off. Really. 

Usually the report will only consist of something like an alert box.

Yes, an alert box displaying some text or maybe just the number '1'. This is the proof of concept that demostrates JavaScript execution was possible using the functionalities of your vulnerable web application.

Now tell your Penetration Tester to weaponize his proof of concept and compromise your user for entertainment sake. That will be another story.

There are many things to consider when one truly wants to exploit the XSS issue and compromise another user. Additional information such as:
- Does the application has some kind of Content-Security-Policy set?
- Is the Session Cookie protected by 'httpOnly'?
- Wait... Are you sure it is not a Self-XSS to begin with?

There are a lot of other examples, such as impactful vs no-impact CSRF attacks, SQL Injections (yeah sleeping the db for 5 seconds. can data really be exfiltrated?), etc etc. You get the point.

An example of easy to spot, easy to exploit vulnerability will definitely be the Insecure Direct Object Reference (hereafter IDOR) vulnerability.

On layman terms:
>This refers to how the application is retrieving information from a backend database, without performing any authorization checks.

For example, imagine the below syntactically incorrect SQL query:

`SELECT * from user_info WHERE user_id = ?`

So when a user logs in, the application will retrieve the user id for the user and returns the user id back. When the user views a page on the web application, the corresponding URL on the browser may look similar to this:

`https://www.example.com/edit/user-info/userid/101`

This means that the user that is logged in has the user id of 101. This is a very common design pattern especially for MVC (Model-View-Controller) frameworks. Effectively, the backend query that is displaying the authenticated user information will be as follows:

`SELECT * from user_info WHERE user_id = 101`

Put on your hacker hat and think, how can we abuse this? Yes yes yes. Simply by changing the URL on the browser from:

`https://www.example.com/edit/user-info/userid/101`

To:

`https://www.example.com/edit/user-info/userid/102`

Horray, you just have access to another user's (102) potentially private information.

This is an extremely common vulnerability. It is easy to spot, easy to "exploit", and often has very severe consequences. Usually when one IDOR is discovered, one can safely assume the application will be infested with multiple IDORs.

This always results in all 3 components of compromise:
- Read; viewing other user's information
- Write; Editing other user's information
- Delete; Deleting other user's information

Even in 2018, matured organisations such as Twitter is still suffering from these. They are often seen paying $5000USD ~ $10,000USD for IDORs vulnerabilities from disclosed reports and write-ups from security "researchers", or bug hunters.



