---
layout: post
title:  "Renaming a computer in a domain"
date:   2021-02-08 19:28:31 +0000
author: Josip Bognar
categories: PowerShell, Active Directory
image: /assets/img/ccn.png
comments: true
---

There is always a question about what a proper way is to rename a device that is joined to a domain. From my experience, it is best to remove it from the domain, rename and return it to the domain thou some people just rename it, but it is not necessary a proper way.

This is how I am doing and until now, there was no issue, but it requires a bit more effort:
- Sign into the windows with admin user or local admin, if you use local admin, don’t forget to add .\adminusername.
- On the Windows 10 taskbar, enter “advanced system” inside the Cortana search box. When the search results are loaded, click on “View advanced system settings“.
- On the first tab (Computer Name) go to “Change” button.
- Change option from domain to Workgroup and enter some random name. This will require restarting.
- When Windows restarts, sign in with your local admin(domain admin won’t work).
- Search for PowerShell and open it as an Admin and type the following command.

{% highlight ruby %}
Rename-Computer new_name -force -restart
{% endhighlight %}
<img src="{{ page.image }}">
<br><br>

- After the system is restarted, sign in again with your local admin credentials.
- On the Windows 10 taskbar, enter “advanced system” inside the Cortana search box. When the search results are loaded, click on “View advanced system settings“.
- On the first tab (Computer Name) go to "Change" button.
- Change back to your domain and type in the domain.
- Use your domain admin to make a change when Windows prompts you for credentials.
- Go to Active Directory Users and Computers and remove the old device name from the OU.
- Find a new device name and move it to desired OU and assign back GPO's.
- the SCCM should make change automatically.

Things to have in mind!

It might be good practice to run the GPUpdate command in the CMD terminal if that device needs to go back to the user. Another thing is that you can force the SCCM to faster accept the new device name if you need to put it to a specific device collection. For this, we can go to Control Panel and search for Configuration Manager and on the third tab "Actions" then we can run cycle (Discovery Data Collection Cycle).