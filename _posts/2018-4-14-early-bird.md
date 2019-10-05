---
title: 'What is an Early bird code injection technique?'
date: 2018-4-14
permalink: /posts/2018/4/what-is-an-early-bird-code-injection/
tags:
  - malware
---

Evading anti malware software has always been a challenge for the hackers out there. Anti viruses are getting smarter everyday by using behavior analysis by implementing machine learning algorithms. Now hackers have developed a new code injection technique called Early bird.

In simple words, As the name suggests the malware is injected to a working process early i.e its injected before its main thread starts. This makes the malware undetectable because anti malware engines can  hook the process only after its main thread is started. This early loading of malware before the hook is even placed makes it more powerful.

<h2>How Early bird works ?</h2>
Early bird works because of  windows built-in APC function. An APC (Asynchronous Procedure Calls) function enables a program to execute a code asynchronously with the main thread. Using APC malicious code can be loaded asynchronously before the thread.


Here is the step by step process:
<ol>
 	<li> Create a suspended process of a Windows process (e.g., svchost.exe)</li>
 	<li> Allocate memory and load malicious code into the allocated memory region of the process,</li>
 	<li> Queue an asynchronous procedure call (APC) to the main thread of that process (svchost.exe),</li>
 	<li> Call NtTestAlert function to force kernel into executing the malicious code as soon as the main thread resumes.</li>
</ol>
Security researchers from Cyberbit  found that malware like Carberp and DorkBot uses this technique for AV evasion. You can find more details in their report: <a href="https://www.cyberbit.com/blog/endpoint-security/new-early-bird-code-injection-technique-discovered/">New ‘Early Bird’ Code Injection Technique Discovered.</a>
