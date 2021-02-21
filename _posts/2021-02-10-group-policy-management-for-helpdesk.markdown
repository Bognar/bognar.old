---
layout: post
title:  "Group policy management for Helpdesk"
date:   2021-02-10 22:25:31 +0000
author: Josip Bognar
categories: tech, CMD, Active Directory
image: /assets/img/gpresult.png
comments: true
---
One of the most common things for each engineer who works on the helpdesk, service desk, or desk-side is GPO’s (Group Policy). It is a way how to configure many important settings on user computers or networks and by using the Active Directory we can apply those settings to users, computers, groups of users, and groups of computers.

In a few short examples, we will go through how to check them on local PC, how to apply them, and some issues that might happen.

<img src="{{ page.image }}">
<br><br>
Now, I won't go to the part where we apply GPO's in Active Directory because it is usually part of the WSO team or the Windows Server team. As a helpdesk engineer, the best practice is to give read access to AD for us so you can confirm in AD that the policy is applied or log a ticket/call the WSO team to confirm.

The primary focus in this post is how to apply it, check it, and fix issues.

<b>Apply Group Policy</b>

This is actually really simple, what we need is to open CMD and run the code below:
{% highlight ruby %}
GPUPDATE /force
{% endhighlight %}
After this, we need to turn off the device and turn it on.

<b>Checking if the GPO is applied</b>

{% highlight ruby %}
GPRESULT /r -- to get all
GPRESULT /r /scope:computer --- to get policy's applied for computer
GPRESULT /r /scope:user --- to get policy's applied for computer
GPRESULT /r /s computer_name /scope:computer --- to get policy's applied for remote computer
{% endhighlight %}

<b>The GPO is not applying issue</b>

From time to time, there will be some device that is not picking up the GPO. First, we need to be sure that the GPO is applied in AD and try a few times restarting device. We can also go to Control Panel and search for the Configuration Manager and under "Action" tab, forcing the cycle but if all this fails, we can also try to delete the Group Policy folder in the registry and force applying again.

For this step, you will need admin rights and start the Registry editor. Navigate to the location:
{% highlight ruby %}
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion 
 {% endhighlight %}

and delete the folder called Group Policy.
After this step is finished, try again to run GPUPDATE /force command in CMD, restart the device and the issue should be resolved.

I hope this short info will help someone like junior or entry level employee and good luck.