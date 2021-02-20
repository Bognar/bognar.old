---
layout: post
title:  "How to setup a simple network in Vbox for AD"
date:   2021-02-20 09:15:31 +0000
author: Josip Bognar
categories: tech, Oracle, Virtualization, networking
image: /assets/img/topology.png
---
In one of my previous article, I have explained a bit more about Oracle VirtualBox and today we will talk about how to set up a small network with Active Directory, DNS, and DHCP but only the networking part of the setup, we won't go into details how to install or choose your domain, etc. This will enable us to add other VM's to the domain and play with GPO's.

As can be seen in the image below, we will have two virtual machines(Server and the Client). So for us to start building a network, please be sure that you have created two VM's, one with the Windows Server 2019 and another one with the Windows 10 Pro/Enterprise.

Before we start the server machine, in VirtualBox please go to that machine Settings, then Network, and ensure that Adapter 1 is on bridged mode and turn on adapter 2 and set it to Internal network. For Virtual Machine No 2, change network adapter 1 from NAT to internal network.

Turn on the server machine and install Active Directory, DNS, and DHCP - this part is not explained because there are thousands of tutorials and videos about it.

<img src="{{ page.image }}">
<br><br>

After the installation, reboot the machine and when your back to the device, go to the Server Manager and press on the Local server. At this point, you should already have your domain, pc name set so we will see two NIC cards that have DHCP assigned. Find out which one is external and set all to dynamically assigned IP/DNS for TCP/IPv4.

For the internal NIC we need to setup:
{% highlight ruby %}
IP: 10.0.0.101
Mask: 255.255.255.0
Default Getaway: N/A - empty
Primary DNS: 127.0.0.1
{% endhighlight %}

The next step is to setup DHCP Scope so go back to the Server Manager, press on Tools, and choose DHCP. This will open windows with your domain so expand it and right-click on IPv4 and choose <b>new scope</b>.
We will set up a range of 10.0.0.200 - 10.0.0.250, the default getaway will be 10.0.0.101 and all the rest just leave the default.

Now, if you turn on virtual machine no 2, it will see your network and you can join it to your domain.