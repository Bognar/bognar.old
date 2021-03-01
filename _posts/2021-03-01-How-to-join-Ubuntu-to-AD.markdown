---
layout: post
title:  "How to join Ubuntu to the local AD"
date:   2021-03-01 14:55:31 +0000
categories: Active Directory, Ubuntu, Linux
image: /assets/img/ubuntu-20-04-focal-fossa.jpg
comments: true
---
Today we will see how Ubuntu 20.04 can be joined to the Active Directory and this will be done in the network that we previously set up in the post [HERE]({% post_url 2021-02-20-How-to-setup-a-simple-network-in-VirtualBox %}).
We will need a few things from that post, and you will need to get that information from your server. In my case DNS:10.0.0.101, Domain: Bognar.la, Server: Thor.bognar.la.

<img src="{{ page.image }}">
<br><br>
First thing is to open the terminal and update the system to the latest updates:
{% highlight ruby %}
sudo apt update & sudo apt upgrade -y

# after this we need to disable and stop resolved service.
sudo systemctl disable systemd-resolved.service
sudo systemctl stop systemd-resolved.service
{% endhighlight %}

The next step is to install all packages we need to have, and we need to do this command:
{% highlight ruby %}
sudo apt -y install realmd libnss-sss libpam-sss sssd sssd-tools adcli samba-common-bin oddjob oddjob-mkhomedir packagekit
{% endhighlight %}


Now we need to set the DNS to point to an internal DNS we have set up in our network and that is 10.0.0.101. To do that, we need to edit resolv.conf file and change the IP address under nameserver to 10.0.0.101.
{% highlight ruby %}
sudo nano /etc/resolv.conf
{% endhighlight %}

Now all is set for us to discover and join the domain:
{% highlight ruby %}
sudo realm discover bognar.la
bognar.la
  type: kerberos
  realm-name: BOGNAR.LA
  domain-name: bognar.la
  configured: no
  server-software: active-directory
  client-software: sssd
  required-package: sssd-tools
  required-package: sssd
  required-package: libnss-sss
  required-package: libpam-sss
  required-package: adcli
  required-package: samba-common-bin
{% endhighlight %}

To join the domain, you will need to have an account with domain admin GPO or create one for that:
{% highlight ruby %}
sudo realm join -U Administrator bognar.la
Password for Administrator:
{% endhighlight %}

We also need to make changes for home directories and save the changes:
{% highlight ruby %}
sudo nano /usr/share/pam-configs/mkhomedir

# edit this file so that it looks like this:

Name: Create home directory on logon
Default: yes
Priority: 900
Session-Type: Additional
Session:
        required                        pam_mkhomedir.so
{% endhighlight %}

Now we need to run pam update
{% highlight ruby %}
sudo pam-auth-update
# when the windows popup, chose/select the option "Create a home directory on logon" After saving run another command to allow people to sign into this device.
sudo realm permit --all
{% endhighlight %}
Now after you restart your ubuntu device, you can sign in by using bognar.la\Administrator.