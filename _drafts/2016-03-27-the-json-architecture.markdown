---
comments: true
title: "The JSON Architecture"
date: 2016-02-20 09:00:00
categories: general
---

The JSON Architecture is my original idea and hope to shed light in state management, error handling and async processing for UI systems.

Table of contents
1. Overview
1.1. Motivation
1.2. Technology overview
1.3. Architecture overview
2. Architecture definition
2.1. JSON RFC definitions
2.2. Immutability with cursors
2.3. Streams processing
2.4. Pure views with declarative state bindings
3. Sample Implementation
3.1. BaobabJS setup
3.2. RiotJS setup
3.3. Kefir setup
3.4. RamdaJS setup
3.5. Webpack setup
3.6. Integrating technologies
4. Comparision
4.1. Flux model
4.2. Actor model
4.3. Flow based programming model (CycleJS)
4.4. JSON Architecture
4. Conclusions
4.1. Pure MVC definition
4.1. Complexity analysis
4.2. Opportunities
4.3. Tradeoffs
5. References

# Overview
The current post deals with describing an web UI architecture based on the JSON ecosystem (JSON Data, JSON Patch, JSON Pointer and JSON Schema) with the goal of convincing the reader to adopt declarative techniques for state management, error handing and async processing.

# Motivation
Complexity is advertised as the evident source of confusion and error in the programming world.
These days language creators, as well as library and framework creators, are popularising functional principles to aleviate common errors. The consensus reached is that "state" entangles functionalities, creates dependencies between modules and creates a host of errors, that are numerous, hard to debug and hard to fix.

Traditionally, the OOP movement described the building blocks of applications as state components which cater after their internal state and protect it from being corrupt.
In isolation, these components can be tested and ensuered that their state transformation mechansims work as intentded.
However, when components negotiate state changes between themselves, complex cases arise. Sometimes, another component is needed to mittigate the transaction, other times more logic is added to one or both components.

Through these issues, design patterns emerged with the aim to reduce accidental complexity. They provide a "best practice" approach to a generic scenarios. 
When bundling together these "best practices" we create a development environment that has clear rules and stantardised ways of implementing a generic business domain. In other words, we created frameworks that guide developers on their path, ensure they avoid common "traps" and make complexity manageable. Frameworks can be seen as a fistfull of "complexity reducers" that when used in a precise fashion you will end up with a working application.

However, frameworks have an inherent flaw, they make a basic assumption that complexity cannot be managed any other way but through standardising the writing code. Frameworks make explicit demands on programmers which must obey their rules. The classic way of working with a framework is that, when the developer breaks a (arbitrary) rule the framework swiftly notifies about the mistake and stops functioning altogheter until that mistake was repaired. In this case, the framework did all the thinking before hand and the developer becomes a simple user. His/hers only task is to learn the ins and outs of its rules and figure out all the intrincancies of what someone else thought and follow them for the sake of consistency even when simpler ways are obvious. This is not subtle.


However, the web is championing mental frameworks over traditional frameworks. Web developers have at their disposal one of the largest utility ecosystem in the programming world and, to this extent, programing without industrial frameworks can be seen more frequently. The power of orchestration of small tools based on the mental models enables developers to stay agile and independent rather than trying to push the limits of an existing baseline.

The JSON Architecture, as I'll try to convey in the following post, bridges principles from the functional programming world and the OOP world.
business domain. This, combined with an MVP approach to building software, makes programming a creative experience.

Although the [Flux model](link here) has improved the consesus on how to gain simpler and more structured applications than before there are still many ways it can be improved.

### State is not centralized

### Essential state and derived state are merged
### IF/ELSE branching in components instead of declarative nodes on a centralized system (no side effects/pure components)
### State propagation is sequential and has dependencies

1.2 Technology issues overview
a. Redux - Actions are too abstract and only add complexity
b. CycleJS - State is spread among streams and never located
c. React - Propagating state from parent - children leads to massive complexity

1.3


## Handling Routes

Routes are added on the state tree and dynamic nodes on ui components decide if those components should be visible or not.

Example bellow:
----

In usual routing systems there is a so called "separation of concerns" where the router is separated from the components that should be shown or hidden. The consensus is that components should not know when they are shown but should obey a rulling entity. By having everything in the state object, then the state object becomes the rulling entity and as such we can safely define a direct relationship between the state object and if a component is shown. When composing components we can define on the parent or even inside the component.

A full list of routes can be deducted from the state tree given the dynamic nodes created if they corespond to the `route` signature.

The visibility aspect of a component can be defined simple as `route('/login')` or they can host futher logic through `route('/login', ['user/authenticated'], (route, auth) => not(auth))

