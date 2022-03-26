---
layout: post
title:  "Building a custom wordlist for Brute-Force attacks"
date:   2022-03-26 17:27:30 +0000
categories: Linux, Cybersecurity, Pen-Testing, Themed CTF
image: /assets/img/wordlist.png
comments: true
---
Today I will be talking about a useful tool on Linux called Cewl for creating custom wordlists.
One of the most overlooked things in pen-testing is building a good wordlist to feed it to tools such as John the Ripper or Hydra. 

Those who use Kali or Parrot Linux distros, they already know that under /usr/share/wordlists we can find all kinds of flavours of wordlists to use in pen-testing and brute force attacks. 

<br>
So, why is this actually important?

<br>
Often most fun CTF(Catch the Flag) devices are themed which require you to investigate a specific event, person, songs, literature etc. Another good reason can be a targeted attack on a specific topic, person or company. So it would be really nice to have some option to fast collect words from page, site, document and use it as the source for brute force attack and this is where Cewl comes in.

CeWL (Custom Word List generator) is a ruby app which spiders a given URL, up to a specified depth, and returns a list of words which can then be used for password crackers such as John the Ripper. Optionally, CeWL can follow external links.

CeWL can also create a list of email addresses found in mailto links. These email addresses can be used as usernames in brute force actions.

The app comes pre-installed on distros for cybersecurity and for other distros, it can be installed with: sudo apt install cewl command.

<img src="{{ page.image }}">
<br><br>

The simple usage looks like:
{% highlight ruby %}
cewl https://websitelink > outputfilename.extension
cewl http://www.websitelink -n -e
{% endhighlight %}

If we want to build a list of e-mails from any website(Data mining), we can add flags -e and -n as seen on the code snipped above.
There are many similar scripts and tools out but I find Cewl to be easy, fast and efficient. 


