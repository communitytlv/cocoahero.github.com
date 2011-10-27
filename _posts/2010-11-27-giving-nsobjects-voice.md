---
layout: post
title: Giving NSObject's a Voice
tags: cocoa, objective-c, ios-dev
summary: One of the most common things that I do when debugging code is place various NSLog statements to see where the code is going (or not going).  Very often the string I was printing had information about the current method call and or the object it was being called from.  So I decided to make my life a little easier with a small little extension on NSObject.
---
One of the most common things that I do when debugging code is place various NSLog statements to see where the code is going (or not going).  Very often the string I was printing had information about the current method call and or the object it was being called from.  So I decided to make my life a little easier with a small little extension on NSObject.

Below is the header and implementation files respectively for the extension.

{% highlight objectivec %}
#import <Foundation/Foundation.h>

@interface NSObject (Say)
- (void)say:(NSString *)message;
@end

@implementation NSObject (Say)
- (void)say:(NSString *)message {
    NSLog(@"%@ says, \"%@\"", [self class], message);
}
@end
{% endhighlight %}

Once you have added these files to your project and imported the "NSObject+Say.h" file, all you have to do is call this new method on any object.

For example:

{% highlight objectivec %}
- (void)applicationDidEnterBackground:(UIApplication *)application {
    [self say:@"I just entered the background."];
}
{% endhighlight %}

In the console, you will see something similar to the following.

{% highlight text %}
2010-11-27 22:23:59.000 MyAwesomeApp[4302:207] MyAppDelegate says, "I just entered the background."
{% endhighlight %}

Now your objects have personality! Yeah, it's a gimmick. But it actually makes debugging a lot easier (if not fun). I now have the habit of placing these lines at any major procedure just so I can see what is going on in the background. For example, multi-tasking delegate calls, memory warnings, beginning Core Data context saves, etc. If anything, it gives you human readable "paper trail" when trying to squash bugs other than the raw stack trace.