---
layout: post
title:  "How to install Kali linux to android device"
date:   2021-06-14 18:35:31 +0000
categories: Linux, Android, Cybersecurity
image: /assets/img/kali.jpg
comments: true
---
The last few months I have been focused on cybersecurity and it is hard to not notice that courses like certified ethical hacker (CEH) or any other major certification will suggest you to use some distribution of Linux that is built for cybersecurity and forensics such as Kali or Parrot. Now, you need to understand that you can install any linux and download all those packages that Kali and Parrot have but still, why not have it all on your mobile phone?

 
If you install it on your Android device, you will always have access to it and also, it is just simple and easy to have all that in your pocket. Before we start to dig into how to and a few simple code lines, here are prerequisites needed to start.
 
- Android device with about 10 GB extra internal storage(most new devices have that).
- Download and install Termux app from the google play store [HERE](% link https://play.google.com/store/apps/details?id=com.termux&hl=en_IE&gl=US %).


<img src="{{ page.image }}">
<br><br>
Just so that there is a fine line of clarity, this is not something unsecure but keep in mind that you need a bit of understanding why you need Termux and Kali and also, to be confident about your phone security by having good understanting of these apps and Android OS. It is good to point out that this installation does not require root access!

Rootless Kali linux is being deployed by NetHunter, which is official edition and part of Kali distribution found on [Kali website](% link https://www.kali.org/docs/nethunter/nethunter-rootless/ %).


When you download and install the Termux app, start it and write down these steps in the terminal. 

{% highlight ruby %}
termux-setup-storage
pkg install wget
wget -O install-nethunter-termux https://offs.ec/2MceZWr
chmod +x install-nethunter-termux
./install-nethunter-termux
{% endhighlight %}

This installation will take about 10 minutes and after that you will have access to Kali. To start Kali in terminal mode just type nethunter or nh.
Another good thing is that you can actually run kali with GUI mode. To do that, first we need to setup kex password and port. so we need to type in Termux.

{% highlight ruby %}
nethunter kex passwd
{% endhighlight %}
This will setup the password for VNC server and also it will provide you with the info about the port. If you want to open GUI mode on your mobile phone, just download any VNC viewer and type for the server localhost:port number and your VNC server password.

Why do I have Kali on my phone? 

I have a few laptops with Ubuntu, CentOS and Windows 10 but I wanted to have Kali on a device always close to me. Also, I always have USB-C to Ethernet adapter so I can easy test network over wireless or ethernet cable without making mess of having dual boots.

