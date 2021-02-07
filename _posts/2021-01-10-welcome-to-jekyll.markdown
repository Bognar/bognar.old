---
layout: post
title:  "How to add TinyMCE editor to angular project"
date:   2021-02-06 19:59:31 +0000
categories: Angular, TinyMCE, Web Development
comments: true
image: /assets/img/tinymce.png
---
Hi all, this is my first post on my blog so I wanted to share some tips with you that I caught by doing one of my blog projects.

Why is this important?

To those who have never go deep into posting data to database like firebase real time database or noSQL, this might be really interesting. Sometime we have a need to post whole block of formated data into database, maybe there are some HTML markup's and links etc. So it would be so cool if we could just drop it all to database right? Well, you can post them all under same firebase node in database but many will say "is it ok to post it there with all formatings?" and the short answer is yes, you can! What's more Wordpress, as one of top CMS apps, is doing it also!

How can we do it?

You could use javaScript:

{% highlight ruby %}
getElementById("elementId");
{% endhighlight %}

But there is a simple way how you can do it by using wysiwyg editors like TinyMCE. For angular you can visit https://github.com/tinymce/tinymce-angular.

To add it to your angular project, just run:

{% highlight ruby %}
npm install @tinymce/tinymce-angular
{% endhighlight %}

After that, import it into your module.ts file and add it under imports:
{% highlight ruby %}
import { EditorModule } from '@tinymce/tinymce-angular';
imports: [
    BrowserModule,
    EditorModule // <- Important part
{% endhighlight %}
Now to use it in your HTML you can add this code and check how we implemented two-way binding data to variable.
{% highlight ruby %}
<editor [(ngModel)]="textdata" apiKey="" [init]="{plugins: 'link'}"></editor>
{% endhighlight %}
After that, you can freely use editor to format text and set your typescript code to send data to you database. Api key is provided after you register on TinyMCE webpage.
Hope you had a nice time and if you find this to be useful to you, drop me a message.