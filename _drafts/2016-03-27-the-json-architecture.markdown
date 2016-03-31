---
layout: post
comments: true
title: "The JSON Architecture"
date: 2016-02-20 09:00:00
categories: general
---

The JSON Architecture is my original idea and hope to shed light in state management, error handling and async processing for UI systems.

Table of contents
1. Overview
1.1. Technology overview
1.2. Architecture overview
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
State is, now more than ever, the evident source of confusion and error in the programming world. These days all language creators, as well as library and framework creators, have adopted functional principles to aleviate common errors. It seems that "state" entangles functionalities, creates dependencies between modules and makes errors hard to locate.

OOP describes the building blocks of applications as state components which cater after their internal state and protect it from being corrupt. In isolation, these components can be tested and ensuered that their state transformation mechansims work as intentded. However, when components negotiate state changes between themselves, complex cases arise. Sometimes, another component is needed to mittigate the transaction, other times more logic is added to one or both components.

Design patterns aim to reduce accidental complexity by providing a "best practice" approach to a generic scenarios. When bundling together design patterns you get a framework that gives developers the path on which they need to walk to avoid the "traps" when building complexity. Frameworks can be seen as a fistfull of "complexity reducers" that when used in a precise fashion they will achieve a working application.

However, the web is championing mental frameworks over traditional frameworks. Web developers have at their disposal one of the largest utility ecosystem in the programming world and, to this extent, programing without industrial frameworks can be seen more frequently. Developers are starting to be understand the power of orchestration of small tools based on the mental model achieved from understandin business domain. This, combined with an MVP approach to building software, makes programming a creative experience.

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
