---
layout: post
title: "Standardize variable names"
date: 2015-06-18 09:00:00
categories: functional_programming
---
We should refrain from intertwining context with code (this is an anti-domain logic post):

- if a function needs to transform a solitary value then the argument will be called *value* (regardless if that is pixel, points, users, etc)
- if a function needs to transform an array value (like in reduce, or map) then the arguments are called *past, current*
- If a range needs to be expressed then pass it as *range*

the function name needs to give the context of the arguments and not the other way around.

The effect of this type of standardisation would mean a lot of functions/methods etc will be far easier to reason about as they would have been stripped of their domain logic. Portability and readability of functions would be far greater increased.
