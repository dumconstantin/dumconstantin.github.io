---
layout: post
comments: true
title: "The JSON Architecture"
date: 2016-02-20 09:00:00
categories: general
---
Fixing the modern unspoken architecture problems (with an emphasis on solving Redux, CycleJS and React's)

The JSON Architecture is my original idea and hope to shed light in state management, error handling and async processing for UI systems.

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
