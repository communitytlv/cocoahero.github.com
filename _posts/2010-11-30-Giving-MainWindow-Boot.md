---
layout: post
title: Giving MainWindow.xib the Boot
tags: cocoa, objective-c, ios-dev
---
I will be quick and to the point. I dislike XIB's (Interface Builder documents). Generally, I dislike all WYSIWYG style replacements for raw code. Granted, XIB's are the best solution I've seen in a long time, but they are a pain to load for anything but a UIViewController subclass.

Because of my stubbornness, I immediately had to find a solution to the default MainWindow.xib found in any new Xcode iOS project. And by solution, I mean an alternative method. By default, the MainWindow.xib file is responsible for loading the UIApplicationDelegate object at launch and connecting the single UIWindow instance. Believe it or not, you can get the same result without this file. (Hooray!)

The generic steps are as follows:

1. Delete the MainWindow.xib file.
2. Remove the "Main nib file base name" or "NSMainNibFile" key from your Info.plist.
3. Alter the parameters of UIApplicationMain in your main.m file.
4. Add initialization code to create the UIWindow object.

Trust me it's easier than it sounds. The first two steps are straight forward. The delete key is your friend. For the main.m file, find the line that is similar to

<script src="https://gist.github.com/1111511.js"> </script>

Change it so the last parameter is a string with the class name of your UIApplicationDelegate, like so:

<script src="https://gist.github.com/1111514.js"> </script>

Now all you have left to do is to initialize the UIWindow instance variable yourself. A simple "getter" property implementation fixes this quickly.

<script src="https://gist.github.com/1111517.js"> </script>

*Note* The code above assumes your UIWindow instance variable is named window and you have a property declaration in your AppDelegate's header file.