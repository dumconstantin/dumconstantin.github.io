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



## Definition of view, controller and model
The view does no longer depend on controllers. It does not need to expose anything to the system as it is a sideeffect in itself. The view only needs to listen to state changes from the state object and react accordingly without any computation just proper transformation of data to fit the template.

There is only one controller and one model exposed to the application. All changes that can ever happen in the application are contained solely in the controller. And any change that can ever happen will come only through the controller interface as a JSON patch.

There is only one model that expresses the state of the application. The sub-models represent the branches of the state tree and are completely encapsulated by the state tree. They cannot rely on other sources of data but those found in the state tree.

Controllers will always deliver essential state - state that cannot be derived from other state.
Models will always deliver derived state from the essential state that is delivered by the controlers

The structure of the essential state will be delivered by the JSON schema and thus ensuring a single source of truth regarding paths in the system.

So the esential state is given by the JSON schema and is modified by JSON patches coming from controllers.
Derived state is given by models and is used by either the Views or the Controllers.

# The JSON Architecture changes the way development is being handled
Developing with the JSON Architecture changes the way we imagine building an application. 

Normally you are interested with the end points of the application - The API/The entry points in the application. You then normally enter gracefully in the application following the index method and finding your way through until the model - next the database schema then going back the path looking at the views and in the end you exit the entry point you came in initially. You repeat this process for other methods in the API until you can say you understand how the application works.

Unfortunately, the way the application works is not necessary if you want to **understand** an application. What you really want is to see what it does, in the real world you are first interested in driving the car and the seeing under the hood what the engine does in order to move the car. Its an outside in approach, but we are fooled to think that working outside-in through the API is equivalent to an outside-in approach of understanding the application.

No, we need to understand the end product of the application - which is the state that an application can have at a given moment. What if, at the first day of your new job, you are presented with the idle state of the application. You then proceed on doing actions and see how that state changes in its entirely, how new properties appear or dissapear while you do actions on the application. What if you could also change that state and see how the application behaves when you changed something. Did you break it? Change it back, reverse the state change, and see the application in an identical state as before.
You don't need to understand the processes that make the transition between one state to the other, you ** only ** need to understand what the change is between an action and a reaction. You are doing a mental model on how the application behaves and not how the application works. This makes development intuitive.

You see the application working and understand it better than if you would spend a month learning by heart the API. You can play with the application both from a user level and a programmer level, tweaking with values in the state tree and seeing how that change modifies the application. In some sense, application development becomes a game something fun for you to explore. Something that you can enjoy as you wonder "What will this do if I change it?" and then see the reaction.

After you've played a bit like this with or without a small tutorial that shows you some of the more important states of the application - you then can go deeper and see what are the processes that made the state change like it did when you did that action. But the fun doesn't stop there, because each action is more or less self contained in a single place, in a file which you can tweak as you would - put logs in streams, delete stuff or add processing. Every time you make a change, you can see how the state is being modified after a certain action. You can even revert the change, modify the controller again and see what happens - it really becomes an experience of understandgin rather than a static learning experience.

The effects of this is a greater sense of controller - nothing is out of reach, you fully understood the entire system just by playing with it. There are no hidden parts for you do figure out, everything is visibile from the change it does.

The makes developers more productive - you develop an intuition on how the application will behave when you change the state in a certain way - you start developing intuitively and experimenting on the state tree - thus minimizing the likelyhood of introducing new bugs or architecture issues in the application.

It makes it easy to introduce new developers to the development environment - the approach is not a diffcult process meant for seniors - it is a process of play where the developer learns gradually and becomes and expert in the system in a matter of days and not months or years as you would otherwise have.

# A strong need for a tool for proper state management similiar to what I did with ``` baobab-json-editor ``` that can:
- Track changes in state and be able to unwind and replay them
- Freeze state and reject all patches
- Pause the state and see the queue being formed with other patches.
- Add a debugger before a patch is applied in order to investigate it and the source to which it came from
-- This actually allows the developer to tweak the patch several times until it does what it should
- Live view of what each patch does to the state (e.g. highlight fields - similar to the html inspector in chrome )
- State properties definition. When you hover on a state property you should have a tooltip with a description of what that entity means
- Be able to see all the patches applied, in sequence and be able to click on a patch and the state will be changed to when that patch was applied.
- Be able to see where each patch originated from.
- Be able to search through the patches.
- Be able to export the patches array and be able to play them back somewhere else.
