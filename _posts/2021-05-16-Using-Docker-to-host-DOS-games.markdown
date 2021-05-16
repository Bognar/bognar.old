---
layout: post
title:  "Using Docker to host DOS legacy apps or games"
date:   2021-05-16 22:55:31 +0000
categories: tech, Docker, Linux, Dos
image: /assets/img/docker-aladdin.jpg
comments: true
---
I didn't write any post for almost two months; well, I was sharpening my skills and this time it is something useful. While many companies are still doing the transition from desktop/on-premises apps to a cloud environment, there are still some legacy apps that need to be ported and used. My experience showed me that the biggest issue with legacy applications have companies that are also a long time in business, so containers like Docker are a great and cheap alternative before investing and moving business to a new application on market. 

In the example below, we will show you how to port the old dos game to docker and how to access it using VNC remote connection.

Important! 
1. The file "Dockerfile" has no extension so on Windows OS, create it with any text editor.
2. You need to install Docker from their website.
3. You can clone my repo if you like on link: https://github.com/Bognar/dockeraladdin
4. It is advised to stop docker image if you are not using it and to find images use command 'docker ps -a' and to stop image 'docker stop imageid'
5. This post wont explain how to use docker, only demonstrate possible usage for creating container and hosting DOS apps in it.
6. You might find similar codes on the net but, this codes are working comparing to many blogs posts that had typos or missing extras. 

<img src="{{ page.image }}">
<br><br>
For the start, create a new folder and in that folder, we need to create "Dockerfile". On my Linux, I do 'sudo nano Dockerfile' and then we can copy and paste the code below to the file. We also need to create a folder aladdin for the game so, download it from any google source and extract the game to aladdin folder. As can be seen from the file, we will be using ubuntu 20.04 but you can also use Alpine(smallest Linux distro). 

Other things we will be installing to the docker image is TightVNC Server Ratpoison Dosbox Novnc Websockify.

{% highlight ruby %}
FROM ubuntu:20.04
ENV USER=root
ENV PASSWORD=yourpassword
ENV DEBIAN_FRONTEND=noninteractive 
ENV DEBCONF_NONINTERACTIVE_SEEN=true
COPY aladdin /dos/aladdin
RUN apt-get update && apt-get install -y tightvncserver ratpoison dosbox novnc websockify && \
 mkdir ~/.vnc/ && \
 mkdir ~/.dosbox && \
 echo $PASSWORD | vncpasswd -f > ~/.vnc/passwd && \
 chmod 0600 ~/.vnc/passwd && \
 echo "set border 0" > ~/.ratpoisonrc  && \
 echo "exec dosbox -conf ~/.dosbox/dosbox.conf -fullscreen -c 'MOUNT C: /dos'" >> ~/.ratpoisonrc && \
 export DOSCONF=$(dosbox -printconf) && \
 cp $DOSCONF ~/.dosbox/dosbox.conf && \
 sed -i 's/usescancodes=true/usescancodes=false/' ~/.dosbox/dosbox.conf && \
 openssl req -x509 -nodes -newkey rsa:2048 -keyout ~/novnc.pem -out ~/novnc.pem -days 3650 -subj "/C=US/ST=NY/L=NY/O=NY/OU=NY/CN=NY emailAddress=your e-mail address"
ENV PORT 6080
CMD vncserver && websockify -D --web=/usr/share/novnc/ --cert=~/novnc.pem 6080 localhost:5901 && tail -f /dev/null
{% endhighlight %}

Now that we have the project folder awith Dockerfile and another game folder called aladdin(my choice of the game), we can continue with building and running image.

{% highlight ruby %}
sudo docker build -t aladdin .
sudo docker run -p 6080:6080 aladdin
{% endhighlight %}

After all goes well, we need to open localhost:6080/vnc.html and connect to our docker container. Now you will be presented with DOS so we need to switch to C drive, type the following codes each following with enter button and enjoy the game.

{% highlight ruby %}
c: 
cd dos
cd aladdin
aladdin.exe
{% endhighlight %}

You can also deploy a few games or apps in the same image so we can create more folders for different apps and game but also, we need to add extra commands in Dockerfile to COPY content after 'COPY aladdin /dos/aladdin'. Hope this short intro will give you some extra brain cookies to chew, Cheers!