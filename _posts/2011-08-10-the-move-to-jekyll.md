---
layout: post
title: The Move to Jekyll
tags: jekyll, blogging, github
summary: Last year, I started by blogging journey.  After playing around with a self-hosted WordPress VPS, I knew that I didn't want the administrative headache associated with it; Not for a simple blog anyways.  Enter Jekyll.
---
Last year, I started by blogging journey.  After playing around with a self-hosted WordPress VPS, I knew that I didn't want the administrative headache associated with it; Not for a simple blog anyways.  So I found tumblr, which at first was amazingly hassle free.  There were plenty of free themes available, but I always wanted to create my own "look and feel".  Tumblr's API documentation was sloppy at best, and at around the same time, they were having a TON of outages and server errors.  The other part of the story was I wanted to have more than just a blog on my website.  Something to show projects, contact info, and the like.  Tumblr just didn't fit that bill.

So, I began to dabble with Ruby on Rails.  I had used it before for actual web applications, but realized I could use it to make a semi-dynamic "portfolio" site.  What made it better was the fact that I could use Heroku as a **FREE** hosting platform.  The original app was done with rails 2.3.8.  Then rails 3 came out.  Of course as a developer, I wanted to use the new hotness, so I decided to migrate my app to rails 3.  I then realized that again, I had created a monster that I did not want to have to maintain just to have a blog.

Around the same time as my Rails dilemma, I started using Github more and more.  I then noticed a [particular blog](http://warpspire.com/) that was run entirely using Github pages, and wondered, how do you maintain that?  Enter Jekyll.

Jekyll is a [open source project](https://github.com/mojombo/jekyll) designed and written by Github's own Tom Preston-Werner.  At first, it was a little hard to understand what was going on, but once I figured it out, it was amazing.  There are basically three components to a Jekyll website.

1. Layouts / Templates
2. Posts
3. Static Pages

## Layouts / Templates
Layouts in Jekyll go in a directory called **\_layouts/** (duh).  They are written in HTML and you can use certain predefined "liquid" tags for dynamic elements, such as page title, post date, and content. The best part about them is the ability to have inheritance.

For example, I have a layout called **default** [(_layouts/default.html)](https://github.com/cocoahero/cocoahero.github.com/blob/master/_layouts/default.html).  In here, I put all the boilerplate HTML code for the outside structure of the web site; the stylesheet links, title element, etc.  The most important thing to put in this layout is the *\{\{ content \}\}* liquid tag.  If your familiar with Ruby on Rails, this tag acts like a yield, and is what allows inheritance to work.

Since layouts can have a parent layout, you can refactor "views" into separate layout files, and then have them be merged at compile time.  Accordingly, I have a layout called **post** [(_layouts/post.html)](https://github.com/cocoahero/cocoahero.github.com/blob/master/_layouts/post.html) that has some HTML to layout how the post will look.  In this file, I can use the liquid tags *\{\{ post.title \}\}* and *\{\{ post.date \}\}* to dynamically get the information about the post.

To summarize, you use *\{\{ content \}\}* to yield to a child layout (or static page), and object style accessors to get information about the page or post your rendering.

## Posts
Posts in Jekyll are considered a special type of file.  They exist in the **\_posts/** directory and have a specific naming convention: *YYYY-MM-DD-Hyphenated-Title.{html | markdown}*.  Jekyll parses the filename to get information such post date, and permalink identifier.  They can be written in either HTML or markdown, which will be converted at compile time.

You can set the layout used, title, and *any custom properties* using the "YAML Front Matter" at the top of each file.

## Static Pages
The beauty of Jekyll is in the end, your site is *static*.  That means, any folder structure or static HTML page you create will exist in the final product.  So if you create a folder called **/projects/** with a set of HTML files, you will be able to get to them at *http://yoursite.com/projects/*.  It's that easy.  What could get better? You can use layouts on these too to DRY up your site's code!

## The End Result
As I said before, your final product will be a completely static website.  Jekyll takes all your layouts, posts, and static pages and compiles them together into a special directory called **\_site/**. (It's a good idea to not check this folder into your source code repository unless you plan on deploying that way.)  Depending on your permalink configuration, Jekyll will create folder structures for your posts so you end up with pretty URLs such as http://example.com/2011/01/30/My-Post.html.  And like I said before with static pages, your custom folder structures are preserved and copied into this **\_site/** directory.

## Jekyll and Github pages
Now that I've explained the basics of Jekyll, now for the fun part of hosting on Github!  Simply create a repository called *username.github.com* (obviously substituting your Github username) and push your Jekyll working directory to the master branch.  Github will automatically run Jekyll on your repo and host the resulting site at http://username.github.com.  

For more information about Github pages and Jekyll, please see [here](http://pages.github.com).

