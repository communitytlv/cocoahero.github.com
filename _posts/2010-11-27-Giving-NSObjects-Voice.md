---
layout: post
title: Giving NSObject's a Voice
---
One of the most common things that I do when debugging code is place various NSLog statements to see where the code is going (or not going).  Very often the string I was printing had information about the current method call and or the object it was being called from.  So I decided to make my life a little easier with a small little extension on NSObject.

Below is the header and implementation files respectively for the extension.

<script src="https://gist.github.com/1111543.js"> </script>

<script src="https://gist.github.com/1111546.js"> </script>

Once you have added these files to your project and imported the "NSObject+Say.h" file, all you have to do is call this new method on any object.

For example:

<script src="https://gist.github.com/1111548.js"> </script>

In the console, you will see something similar to the following.

<script src="https://gist.github.com/1111551.js"> </script>

Now your objects have personality! Yeah, it's a gimmick. But it actually makes debugging a lot easier (if not fun). I now have the habit of placing these lines at any major procedure just so I can see what is going on in the background. For example, multi-tasking delegate calls, memory warnings, beginning Core Data context saves, etc. If anything, it gives you human readable "paper trail" when trying to squash bugs other than the raw stack trace.