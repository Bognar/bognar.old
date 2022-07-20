---
layout: post
title:  "How to setup OpenVAS in Docker Container"
date:   2022-07-20 10:04:30 +0000
categories: Linux, Cybersecurity, Docker, Vulnerability management
image: /assets/img/DockerVas.png
comments: true
---
One of the biggest issues in Cybersecurity is not tracking vulnerabilities of your infrastructure and applications, most of the attacks can be prevented by keeping your apps and inventory patched and up to date. I will show you one super fast and easy way to do it by using Docker and OpenVas.

OpenVAS is a full-featured vulnerability scanner developed by the company Greenbone Networks. Its capabilities include unauthenticated and authenticated testing, various high-level and low-level internet and industrial protocols, performance tuning for large-scale scans and a powerful internal programming language to implement any type of vulnerability test.
For more info please visit their [website](https://openvas.org/) 

<img src="{{ page.image }}">
<br><br>

Prerequisite:

Docker needs to be installed on your linux machine.

Add ppa: sudo add-apt-repository ppa:mrazavi/openvas

Install sql: sudo apt install sqlite3


Installing the OpenVAS:
{% highlight ruby %}
docker run -d -p 443:443 --name openvas mikesplain/openvas
{% endhighlight %}
This is related to Docker image located on: https://hub.docker.com/r/mikesplain/openvas/

The next step is jumping into the docker container and updating OpenVAS:
{% highlight ruby %}
docker exec -it openvas bash
## inside container

export FEED=feed.community.greenbone.net
export COMMUNITY_NVT_RSYNC_FEED=rsync://$FEED:/nvt-feed
export COMMUNITY_CERT_RSYNC_FEED=rsync://$FEED:/cert-data
export COMMUNITY_SCAP_RSYNC_FEED=rsync://$FEED:/scap-data

greenbone-nvt-sync
openvasmd --rebuild --progress
greenbone-certdata-sync
greenbone-scapdata-sync
openvasmd --update --verbose --progress

/etc/init.d/openvas-manager restart
/etc/init.d/openvas-scanner restart
{% endhighlight %}

The Feed section is used to get latest info about CVE's but considering this docker image is older then three years, the feed has been changed so we need to update it. After this step is finished, we are ready to access the OpenVas from your browser by going to 127.0.0.1 and signing in with un/pwd:admin

Just a few small tips:
{% highlight ruby %}
List docker containers: docker ps -a
Stop docker container: docker stop "container id"
Change admin password from container: openvasmd --user=admin --new-password=<new password>
Get list of users: openvasmd --get-users
Create a new user:openvasmd --create-user=dookie
{% endhighlight %}

The OpenVAS is free, but the Greenbone Networks company has enterprise-level edition also. This is maybe not the best solution when it comes to security, but it is free and much better than having nothing. Some alternative solutions are Qualys, Nessus, Intrude, Zscaler and most of them cost a few thousand monthly.