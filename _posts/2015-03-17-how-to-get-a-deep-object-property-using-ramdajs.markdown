---
layout: post
title: "How to get a deep object property without recursivity using RamdaJs"
comments: true
date: 2015-03-17 09:00:00
categories: functional-programming
---
A long time ago a friend and colleague of mine made an Object.prototype method to ease JavaScript JSON access. The problem he solved was that if you want to get a deeply nested property from an object you would have to add a lot of conditionals to test each step of the prototype chain. He made the following Object.prototype method:

{% highlight javascript %}
var timestamp = result.getValueOf('header.expiry.timestamp', new Date().getTime())
{% endhighlight %}

It’s terse and elegant. You can find the original implementation at the end of the post.

I want to put up a challenge and find a way to do it in FP instead of using an imperative way. We’ll be relying on RamdaJS to help us compose the helper. This is what we’ll be end up with (you can use this in your project too!):

{% highlight javascript %}

var R = require('ramda') // nodejs module
var getProp = R.curry(function (props, defaultValue, obj) {
    return R.defaultTo(
        defaultValue 
        , R.reduce(
            R.ifElse(
                R.is(Object)
                , R.flip(R.prop)
                , R.always(undefined)
                )
            , obj
            , R.split('.', props)
            )
        )
})
 
var obj = { a: { b: { c: { d: 'nice!' } } } } 
console.log(getProp('a.b.c.d', 'defaultValue', obj)) // logs "nice!"
console.log(getProp('a.b.x', 'defaultValue', obj)) // logs "defaultValue"

{% endhighlight %}

Ok, let’s see what we did there.

To understand the above code you will need to parse if from inside out and right to left:

1) The first thing that happens in the above function is:
{% highlight javascript %}
var propsArr = R.split('.', props) // ['a', 'b', 'c', 'd']
// R.split is just a curried version of [].split method
{% endhighlight %}

2) Next we compose the function that will evaluate if our property exists on the object:
{% highlight javascript %}
R.ifElse(
    R.is(Object)
    , R.flip(R.prop)
    , R.always(undefined)
)
{% endhighlight %}

Here we see why curring is such a wonderful paradigm:
{% highlight javascript %}
var isFn = R.is(Object)
isFn(2) // false
isFn({}) // true
 
R.prop('a', { a: 'foo' }) // 'foo'
R.prop('b', {}) // undefined
 
var flipProp = R.flip(R.prop) // reverses the order of arguments in R.prop
flipProp({ a: 'foo' }, 'a') // 'foo'
// In our example the R.reduce function calls using (obj, prop) while R.prop needs (prop, obj)
// this is why we just flip it and it will now be compatible
 
var alwaysFn = R.always('foo') // very useful for passing a value to a chain of functions
alwaysFn() // 'foo'
alwaysFn() // 'foo'
// In our case we want to return undefined which will trigger false on R.is(Object)
 
var ifElseFn = R.ifElse(R.is(Object), function (val) { console.log(val) }, function (val) { console.error(val) })
isElseFn({ a: 'foo' }) // logs { a: 'foo' }
isElseFn('a') // gives error 'a'
{% endhighlight %}

3) We then iterate on the ifElseFn using the (obj, propItem) arguments:
{% highlight javascript %}
R.reduce(ifElseFn, obj, propsArr)
{% endhighlight %}

*Note*: We use reduce instead of a foreach so that we get only one value at the end of the iteration

4) We then evaluate the result and set the default if we didn’t get a value:
{% highlight javascript %}
R.defaultTo(defaultValue, R.reduce(..))
{% endhighlight %}

Which is a very convenient way to check for both undefined and null:

{% highlight javascript %}
R.defaultTo('a', undefined) // 'a'
R.defaultTo('foo', 'bar') // 'bar'
{% endhighlight %}

And there you have it. No assignments and no imperative error checking just plain and clean FP in action.

Extra: 5) We also curried the getProp function so that we can use it as:

{% highlight javascript %}
R.map(getProp('header.meta.author', 'Anonymous'), posts)
{% endhighlight %}

Which makes the function even more versatile.

Extra: 6) The version my friend did is:

{% highlight javascript %}
//
// getValueOf
// Retrieves the value of a chained Object properties
//
Object.defineProperty(Object.prototype, 'getValueOf', {
    enumerable : false,
    value : function(params, fallback) {
        var value;
        if ('function' !== typeof params && 'string' === typeof params) {
 
            try {
                eval('value = this.' + params.toString());
                if (undefined === value) {
                    throw new Error('not available');
                }
            } catch (e) {
                if (undefined !== fallback) {
                    return fallback;
                }
                return undefined;
            }
        } else {
            return false;
        }
        return value;
    }
});
{% endhighlight %}

Let me know what you think, maybe there are ways to simplify the getProp function even further.
