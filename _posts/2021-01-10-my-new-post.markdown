---
layout: post
title:  "Using Augmented Reality in Projects"
date:   2021-02-07 15:53:31 +0000
categories: tech, Web Development
author: Josip Bognar
image: /assets/img/arjs.png
---
Today I will show you a few simple steps to create augmented reality effect on your website by using ar.js. 
Thanks to Jerome Etienne repo: ar.js
Also obj and mtl files from Ben Desai @ poly.google.com

{% highlight ruby %}
<script src="https://aframe.io/releases/0.8.2/aframe.min.js"></script>
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/1.6.2/aframe/build/aframe-ar.js"></script>
  <body style='margin : 0px; overflow: hidden;'>
    <a-scene embedded arjs>
  <a-marker preset="hiro">
  </a-marker>
  <a-entity camera></a-entity>
    </a-scene>
  </body>
{% endhighlight %}

<img src="{{ page.image }}" class="postimage" alt="post image"> <br>

After this is implemented, we need to add objects inside a-maker tags. As already mentioned, I will use obj and mtl files downloaded from poly.google.com. Before we add code inside tags, we need to upload it to github account and use link to raw data of obj and mtl files. To do that, after we upload files, click on each file and on the right side there is option raw. Now we just copy url and paste them in our code as seen below.


{% highlight ruby %}
<a-entity 
     obj-model="obj: url(https://raw.githubusercontent.com/Bognar/3dobje/master/assets/img/model.obj); 
     mtl: url(https://raw.githubusercontent.com/Bognar/3dobje/master/assets/img/materials.mtl)">
 </a-entity>
{% endhighlight %}

Now you can open this html on your laptop or mobile phone and point your camera to image from this link.
Image can be printed, opened in browser or mobile phone.

