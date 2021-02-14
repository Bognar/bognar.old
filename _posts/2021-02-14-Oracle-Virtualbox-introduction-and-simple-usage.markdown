---
layout: post
title:  "Oracle VirtualBox: The Simple usage"
date:   2021-02-14 21:15:31 +0000
author: Josip Bognar
categories: tech, Oracle, Virtualization
image: /assets/img/vbox.jpg
---
If you are working in any branch of IT, you have got in touch with virtual machines or software to create them. In this post, I will go in short with the Oracle VirtualBox, a cross-platform virtualization application that can be run on Windows, Mac OS X, Linux, or Oracle Solaris operating systems (OSes).
Now, this software is free and will extend the capabilities of your existing computer so that it can run multiple OSes, inside multiple virtual machines, at the same time. 

A lot of companies are using virtual machines hosted on AWS, Google, IBM, Microsoft Azure and other cloud platforms.

The VirtualBox is a cool thing because as a technician or engineer, you can create your own virtual lab and test things like scripts, network subnetting, Active Directory and GPO testing, security penetrations testing's, etc.

<img src="{{ page.image }}">
<br><br>

To get the VirtualBox, you can navigate to <a href="https://www.virtualbox.org/">https://www.virtualbox.org/</a> and download it from the website. On Linux, you can go to your app store and search for it or use the code below.
{% highlight ruby %}
sudo apt-get install virtualbox
sudo apt-get install virtualbox—ext–pack
sudo adduser %username vboxusers ---this will resolve the issue with not recognizing usb drives or media.
{% endhighlight %}

Creating a new VM is simple, and it can be done by using the wizard after pressing on "New" button. Depending on desired OS, there are already pre-built profiles for some usual and most used operating systems and their flavors. There are also some things to keep in the mind, never assign more resources than you have on your system, and don't forget that you need to maintain the smooth work of the host operating system.

The creation of the VM is easy, but if you get stacked please go to the official documentations <a href="https://www.virtualbox.org/manual/UserManual.html#intro-starting-vm-first-time">HERE.</a>

From my experience, many companies tend to overlook candidates on a job interview if they mention Oracle VirtualBox and they expect the experience of using VMWare or Hyper-V. This is a really bad thing because VDI files(virtual machine file extension) can be imported to any other software and though the app looks simple, it is a powerful tool.

The greatest benefits of using this tool are:
- It is free.
- Well supported and updated on regular basis.
- Easy to use and jump into virtual machines.
- Give us the possibility to test things before using them in a live environment.
- Expanding knowledge without worry when we want to try something new.

Hope this small intro will give you some ideas if you still didn't dive into the world or the Virtual Machines. For those who are already using the VirtualBox, you might also try <a href="https://github.com/hyperbox/hyperbox">Hyperbox</a>, Open-source Virtual Infrastructure Manager.