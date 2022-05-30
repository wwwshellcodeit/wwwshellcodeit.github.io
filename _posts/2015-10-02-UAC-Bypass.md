---
title: 		"UAC Bypass: Windows 7 and Windows 8.1"
date:		2015-10-02
tags:		[posts]
excerpt: 	"This is my first article, I hope you like it!"
---
(At the end you will find the commands used)

**Target 1: Windows 7 x64 build 6.1.7601**

Suppose you have a limited shell, our user is part of the "Administrators" group
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass1.png" alt="">

but we can't perform privileged operations
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass2.png" alt="">

let's bypass UAC!

First we create a DLL containing a reverse shell:
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass3.png" alt="">

From our limited shell we can download the DLL with powershell:
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass4.png" alt="">

Now we use wusa to move the dll into a privileged dir(sysprep):
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass5.png" alt="">

We can see that the file has been successfully moved
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass6.png" alt="">

Let's run sysprep.exe and listen with 'nc':
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass7.png" alt="">

Now we have bypassed the UAC and we can create a new user!
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass8.png" alt="">
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass9.png" alt="">
