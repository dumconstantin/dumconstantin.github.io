---
layout: post
title: "Micro modularized CSS framework"
date: 2015-05-18 09:00:00
categories: css
---
To make working easier and more consistent between different parts of the application I think we need to avoid duplication of writing the same styling properties multiple times and instead of using composition to define custom behaviour.

I propose a simple framework using a simple class name scheme:

Style components

{% highlight css %}
.[style_object]-[?type]-[?modifier]
{% endhighlight %}

[style_object]- is the name given to a group of property modifications (e.g. icon, spacing, text, etc)

[type] - is the definition given to the style object (e.g. icon-email, text-secondary)

[modifier] - is what makes the behaviour of style object custom (e.g icon-email-sm-t-l, text-secondary-h-c-lg)

Example modifiers are:

* -l -> left
* -r -> right
* -t -> top
* -b -> bottom
* -c -> center
* -v -> vertical
* -h -> horizontal
* -sm -> small
* -md -> medium
* -lg -> large

They can be joined together to form:

* -t-r -> top right
* -b-l -> bottom left
* -v-c -> vertical center

Examples:

{% highlight html %}
<!-- Place a small Email icon at the vertical center of the current element -->
<div class="icon-email-sm-v-c"></div> 

<!-- Make a block of text be the “Fenice” font with a small (12px) height and also center it horizontally -->
<div class="text-secondary-sm-h-c"></div>

{% endhighlight %}
