---
layout: post
comments: true
title: "The JSON Architecture"
date: 2016-02-20 09:00:00
categories: general
---
Fixing the modern unspoken architecture problems (with an emphasis on solving Redux, CycleJS and React's)

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
The current post deals with describing an web UI architecture based on the JSON ecosystem (JSON Data, JSON Patch, JSON Pointer and JSON Schema) with the goal of convincing the reader to adopt declarative techniques when dealing with state management, error handing and async processing.

# Motivation
State has become, now more than ever, the evident source of confusion and error in the programming world. To this aspect all language creators, as well as library and framework creators, have adopted functional principles to aleviate most of the issues that developers deal with on a regular basis. It seems that "state" entangles functionalities. creates dependencies between modules and makes errors hard to locate.

In the traditional OOP approach, every component has state and conversely every component needs to protect it from being corrupt. In isolation, these components can be tested and ensuered that their state transformation mechansims work as intentded. However, when components negotiate state changes between themselves, complex cases arise. Sometimes, another component is needed to mittigate the transaction, other times more logic is added to one or both components. Design patterns aim to reduce accidental complexity by providing a "best practice" approach to a generic scenarios. What results from design patterns are frameworks that give the developer a series of "complexity reducers" that are used in a certain fashion to achieve a working application.

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
