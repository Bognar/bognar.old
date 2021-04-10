---
layout: post
title:  "How to add TinyMCE editor to angular project"
date:   2021-02-06 19:59:31 +0000
categories: Angular, TinyMCE, Web Development
author: Josip Bognar
comments: true
image: /assets/img/tinymce.png
---
Hi all, this is my first post on my blog, so I wanted to share some tips with you that I caught by doing one of my blog projects.

Why is this important?

To those who have never go deep into posting data to databases like firebase real-time database or NoSQL, this might be interesting. Sometimes we have a need to post a whole block of formatted data into the database, there are some HTML markups and links, etc. So, it would be so cool if we could just drop it all into the database, right? Well, you can post them all under the same firebase node in the database, but many will say “is it ok to post it there with all formatting?” and the short answer is yes, you can! What’s more, WordPress, as one of the top CMS apps, is doing it also!

How can we do it?

You could use JavaScript:

{% highlight ruby %}
getElementById("elementId");
{% endhighlight %}

But there is a simple way how you can do it by using WYSIWYG editors like TinyMCE. For angular, you can visit https://github.com/tinymce/tinymce-angular.
<img src="{{ page.image }}" class="postimage" alt="post image"> <br>
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
After that, you can freely use the editor to format text and set your typescript code to send data to your database. The API key is provided after you register on the TinyMCE webpage.
Hope you had a nice time and if you find this to be useful to you, drop me a message.
