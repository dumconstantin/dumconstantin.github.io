---
layout: post
title: "Add RamdaJs functions to the prototype and global"
comments: true
date: 2015-06-19 09:00:00
categories: functional_programming
---
So that you can then write

{% highlight javascript %}
var a = [obj1, obj2, obj3, obj4]
a.filter(pipe(prop('foo'), eq('pending')).sortBy(prop('no')).last()
{% endhighlight %}

Which is as awesome as it can get and doesn't break the functional programming paradigms.

The object is never mutated. You can think of it as the object would create a namespace for himself so


{% highlight javascript %}
R.prop('foo')(obj) 
// would mean the same thing as 
obj.prop('foo')
{% endhighlight %}

I see the only problem to fix is that the default prototype methods need to be overwritten in order to achieve consistency - which is something that I believe is a good thing as long as you put up a GIGANT poster that your JavaScript application is non-standard and that you can still call the real native functions

{% highlight javascript %}
[].forEach // will call the native 
[]._forEach // will call the curried Ramdajs function
{% endhighlight %}

Better YET would be to declare the underscore for RamdaJS functions to avoid this conflict in the first place

{% highlight javascript %}
a.filter(pipe(prop('foo'), eq('pending')).sortBy(prop('no')).last()
// becomes
a._filter(pipe(prop('foo'), eq('pending'))._sortBy(prop('no'))._last()
{% endhighlight %}

Although it looks way uglier than before - I would really keep the overwrites with a native namespace - I care more about the code I write usually and read than the one that I would use only in edge cases.
