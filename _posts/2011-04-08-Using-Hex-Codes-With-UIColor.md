---
layout: post
title: Using Hex Codes With UIColor
tags: cocoa, objective-c, ios-dev
summary: Being a transplant from web design and development, I have always struggled with converting from hexadecimal representations of colors to RGB.  Usually when I am designing an iOS application, I try to use colors that I have used in web designs.  The fact that I had to convert hex codes into RGB values annoyed me.
---
Being a transplant from web design and development, I have always struggled with converting from hexadecimal representations of colors to RGB.  Usually when I am designing an iOS application, I try to use colors that I have used in web designs.  The fact that I had to convert hex codes into RGB values annoyed me.

So, with the help of [@iMacthere4iAm](http://twitter.com/iMacthere4iAm), we fixed that. =)

In my common code library for iOS, I added an extension for the UIColor class.  In this extension, I created a new factory method that takes a hexadecimal (integer) and an alpha value and returns an autoreleased UIColor object.

{% highlight objective-c linenos %}
// Returns an autoreleased UIColor object
UIColor * myColor = [UIColor colorWithHexCode:0x336699 alpha:1.0f];
{% endhighlight %}

Above is a code snippet demonstrating its use.