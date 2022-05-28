---
layout: post
title:  "Usage of SHA and MD5 to verify file authenticity"
date:   2022-05-28 20:24:30 +0000
categories: Linux, Cybersecurity, Hashing, Malicious software
image: /assets/img/hash.jpeg
comments: true
---
Today we will highlight the importance of Hashing and how it can prevent cybersecurity incidents/events to happen. Some of the most popular hashing algorithms are MD5, which was created by MIT professor Ronald Rivest back in 1991 and SHA256 (Secure Hash Algorithm) developed by the United States National Security Agency. 
The MD5 is still in use, but SHA256 is more secure having 256bits instead of 128bits that we have in MD5. When dealing with new things I always ask myself "Why would I need this and when would I need this?" which are two really important questions.

<img src="{{ page.image }}">
<br><br>

How are hashes generated?

In a simple example below, we have created a file with some text in it and by using the sha256sum application we can get the hash of the file. After that, we went back to the file to edit it and added a few more lines. As we can see after, the hash has been changed so, if the original file has been tempered, hashes won't be the same.

{% highlight ruby %}
josip@:-):~/Downloads/sha256$ nano sha.txt
josip@:-):~/Downloads/sha256$ sha256sum sha.txt 
f33ae3bc9a22cd7564990a794789954409977013966fb1a8f43c35776b833a95  sha.txt
josip@:-):~/Downloads/sha256$ nano sha.txt
josip@:-):~/Downloads/sha256$ sha256sum sha.txt 
c90c2b2e862435474a9dcd10923f6115b4e0e3fdc742b243ab0653883762dbe4  sha.txt
josip@:-):~/Downloads/sha256$ 
{% endhighlight %}

Let's imagine a scenario where you were browsing the net to find a network protocol analyzer. People usually go to a search engine and try to find examples, read forums, chats or some review. Some website made a great review of the Wireshark and you decided to download it by clicking on the link on that website, which may or may not lead to the official website for the software. How can we be sure that this installer is not tempered and is the app created by the developer itself? Well, we can always go to the developer website and look for MD5 or SHA256 keys and compare them to the keys that the downloaded file has.


In a case of the Wireshark we can find those hashes by browsing to https://www.wireshark.org/download/SIGNATURES-3.6.5.txt and below is one of the examples of hashes for 64-bit windows version of the app.

{% highlight ruby %}
Wireshark-win64-3.6.5.exe: 77462328 bytes
SHA256(Wireshark-win64-3.6.5.exe)=042b59e0d28ec9147dd3f94c3f3c82e6e5c3303de50a8fbc06878de9bd3b5e68
RIPEMD160(Wireshark-win64-3.6.5.exe)=ba047c3ca45335da9851a11ac5943ea5637b7d4c
SHA1(Wireshark-win64-3.6.5.exe)=d68cdc4e44371fd126bd667158f9c1d35e3ef3c4
{% endhighlight %}

If we want to check the hash from windows powershell we can do it by using Get-FileHash cmdlet:

{% highlight ruby %}
PS /home/josip> Get-FileHash kk.txt

Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
SHA256          C0FECFC80C7AB63BE59163703231C7819F0009C3438AFFA64C2601A9C0C3AC66       /home/josip/kk.txt

PS /home/josip> 
{% endhighlight %}

What if the hashes do not match?

In a case where the hashes are not the same, the file has been tempered so delete it or you can also copy the hash and search it on https://www.virustotal.com. This website inspects items with over 70 antivirus scanners and URL/domain blocklisting services and it might identify and give us more details about the malicious file.

We won't go into digital forensics too much, but this is a first step that every IT person can do to better protect his environment.





