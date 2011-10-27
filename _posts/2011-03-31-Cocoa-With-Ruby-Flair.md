---
layout: post
title: Cocoa With Ruby Flair
tags: cocoa, objective-c, ruby, ios-dev
summary: After working with the Ruby on Rails framework, there were a lot of things that I noticed about Ruby that I loved.  One of the biggest things was the tight integration of iterations and blocks.  So I gave Cocoa some Ruby flair.
---
After working with the Ruby on Rails framework, there were a lot of things that I noticed about Ruby that I loved.  One of the biggest things was the tight integration of iterations and blocks.

In Ruby, if you have an array, iterating over each element and doing something to the element is as easy as

{% highlight ruby %}
myArray.each do |element|
    puts element
end
{% endhighlight %}

Moving back to my iOS development work and Cocoa, having to use the traditional "foreach" loop seemed archaic.  So I decided to do some hacking and came up with an extension for NSArray.

{% highlight objectivec %}
#import <Cocoa/Cocoa.h>

@interface NSArray (Each) 
- (void)each:(void(^)(id object))block;
@end

@implementation NSArray (Each)
- (void)each:(void(^)(id object))block {
	for (int i = 0; i < [self count]; i++) {
		block([self objectAtIndex:i]);
	}
}
@end
{% endhighlight %}

Now, if you have an NSArray (or NSMutableArray), you can simply call and pass it a block with a single parameter.  The method will then behind the scenes loop over each element and pass the element in as the parameter in your block. =)