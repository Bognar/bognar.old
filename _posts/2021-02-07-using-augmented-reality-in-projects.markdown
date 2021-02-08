---
layout: post
title:  "Using Augmented Reality in Projects"
date:   2021-02-07 15:53:31 +0000
categories: tech, Web Development
author: Josip Bognar
image: /assets/img/arjs.png
---
Augmented reality (AR) was one of the biggest technology trends of 2017 and while many developers still are trying to find a good online library, there are a few scripts out there that can give us really nice effects.

Today I will show you a few simple steps to create an augmented reality effect on your website by using ar.js. 
Thanks to Jerome Etienne repo: <a href="https://github.com/AR-js-org">https://github.com/AR-js-org</a>, and also OBJ and MTL files from Ben Desai @ poly.google.com

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

After this is implemented, we need to add objects inside a-maker tags. As already mentioned, I will use OBJ and MTL files downloaded from poly.google.com. Before we add code inside tags, we need to upload it to the GitHub account and use links to raw data of OBJ and MTL files. To do that, after we upload files, click on each file, and on the right side, there is option raw. Now we just copy URL and paste them into our code as seen below.


{% highlight ruby %}
<a-entity 
     obj-model="obj: url(https://raw.githubusercontent.com/Bognar/3dobje/master/assets/img/model.obj); 
     mtl: url(https://raw.githubusercontent.com/Bognar/3dobje/master/assets/img/materials.mtl)">
 </a-entity>
{% endhighlight %}

Now you can open this HTML on your laptop or mobile phone and point your camera to the image from <a href="https://jeromeetienne.github.io/AR.js/data/images/HIRO.jpg">this link.</a>
The image can be printed, opened in a browser or mobile phone.

Here is the link to working codepen: <a href="https://codepen.io/iFun_Studios/pen/XGzewv">https://codepen.io/iFun_Studios/pen/XGzewv</a>
