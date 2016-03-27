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

1. Overview
1.1 Problems overview:
a. State is not centralized
b. Lack of standardisation of Essential state, derived state and accidental derived state
c. IF/ELSE branching in components instead of declarative nodes on a centralized system (no side effects/pure components)
d. State propagation is sequential and has dependencies

1.2 Technology issues overview
a. Redux - Actions are too abstract and only add complexity
b. CycleJS - State is spread among streams and never located
c. React - Propagating state from parent - children leads to massive complexity

1.3
