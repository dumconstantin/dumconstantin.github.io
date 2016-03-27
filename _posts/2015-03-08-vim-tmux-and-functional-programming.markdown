---
layout: post
title: "Vim, Tmux and Functional Programming"
comments: true
date: 2015-03-08 09:00:00
categories: general
---
I have my hands full. I started learning vim, tmux and many terminal aliases. Shifting my programming paradigms to Functional Programming. I’m aiming towards productivity and code reusability and already I can see benefits from these changes but still, I’m climbing the steep learning curve.

Learnt so far:

* Vim is both a text tool and a language.

It understands sentences like “delete all characters starting from the current position until the first occurrence of the @ character” which in vim language would be dt@ which means delete to @. Amazing right?

I’ve been clicking buttons and keyboard shortcuts all my life, Vim changes all that into a dialog. It already feels more personal than your regular IDE.

* Tmux is like a logistics assistant for software craftsmanship – it manages your work environment, open ssh connections, vim instances, terminal panels, etc. 

I’ve been living on OSX for a few years now and window management was always cumbersome.

I tried SizeUp and currently I’m using Spectacle but still gives aches when handling multiple work environments . I decided to segregate responsibilities – Spectacle for desktop use and Tmux for everything work related. To accomplish this I’m also trying to keep as many programs in the terminal as possible. For example, I now find using FTP from the terminal much cleaner than working with FileZilla.

* Functional Programming (FP) feels so natural.

I was never really an OOP groupie, I guess something just didn’t seem right in that workspace. Several years back, understanding JavaScript and really getting into Event Driven Programming I saw little meaning in grouping data manipulation in objects when in reality data needs to flow without constraints from every place to any place of an application.

As I started grasping FP better I got the insight of composition. I finally understood why all other programming paradigms use Static Typing and State wrong.

- Types are like the contour of puzzle pieces. This allows pieces to only be compatible with pieces that have their counterpart contour.

- State and mutation in the global scope, being eliminated, makes the puzzle a single, clear and always the same image. OOP makes the image on the box cover of your 1000 piece puzzle always change a little bit from one minute to the other. Good luck chasing those pieces.

Anyway I’m at the very start. The above is my initial insight, I’m sure I’ll need to reevaluate my claims once I embrace a hybrid FP OOP Imperative Event driven architecture :)
