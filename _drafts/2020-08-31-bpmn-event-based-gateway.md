---
layout: post
title: "BPMN Event-based Gateway"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, event-based gateway]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Event-based Gateway article provides a detailed explanation of the event-based gateway element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents 
{:toc .large-only}

The BPMN Event-based Gateway article focus on the definition and usage of the event-based gateway element as documented 
in the BPMN 2.0 specification. The example process diagram illustrates the correct use of the event-based gateway. The 
BPMN Guidelines section contains a detailed set of rules that apply to the event-based gateway and explains how the 
element may or may not be used within the different BPMN diagrams.

## What is an Event-based Gateway?
> "The Event-Based Gateway represents a branching point in the process where the alternative paths that follow the 
> gateway are based on events that occur, rather than the evaluation of expressions using process data (as with an 
> Exclusive or Inclusive Gateway). A specific event, usually the receipt of a message, determines the path that will 
> be taken. Basically, the decision is made by another Participant, based on data that is not visible to Process, thus, 
> requiring the use of the Event-Based Gateway." ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Event-based Gateway element using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Event-based Gateway | The Event-Based Gateway represents a branching point in the Process where the alternative paths that follow the Gateway are based on Events that occur. | <iconify-icon height=48px icon="bpmn:gateway-eventbased"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Event-based Gateway
{:.figcaption}

## Understand Event-based Gateway
The event-based gateway does not use the evaluation of an expression to determine the branching point within a process 
as with an exclusive gateway or inclusive gateway. The event-based gateway represents a branching point where the 
alternative paths are based on events that occur. The elements that are the target of the gateway's sequence flows, form
part of the configuration of the event-based gateway and determines the behaviour of the gateway. The target elements 
can be a number of intermediate events (signal, message, timer, conditional & multiple) and Receive Tasks.

The event-based gateway can be seen as a race condition since only one event can be triggered. Once the first event 
(or receive task) associated with the gateway is triggered, the token will travel down the sequence flow of that event 
and all the remaining paths will no longer be valid.

## BPMN Diagram
The following is an example of a BPMN Event-based Gateway within a diagram:

![BPMN Event-based Gateway](/assets/images/posts/bpmn-event-based-gateway/bpmn-event-based-gateway.gif){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Event-based Gateway
{:.figcaption}

## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN element.

* The Event-based Gateway is a diamond that MUST be drawn with a single thin line.
* The Event-based Gateway marker MUST look like a catch Multiple Intermediate Event.
* The Event-based Gateway MUST have two or more outgoing Sequence Flows.
* If Message Intermediate Events are used in the configuration, then Receive Tasks MUST NOT be used in that configuration and vice versa.
* Receive Tasks used in an Event Gateway configuration MUST NOT have any attached Intermediate Events.
* The Event-based Gateway MAY use the following valid intermediate event triggers: Message, Signal, Timer, Conditional, and Multiple (which can only include the previous triggers). 
* The Event-based Gateway MAY NOT use the following valid intermediate event triggers: Error, Cancel, Compensation, and Link.
* Target elements of an event-based gateway MUST NOT have additional incoming Sequence Flows.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* The event-based gateway should not be labelled, but all the subsequent events should have labels.

## Finally
This article provided a detailed explanation of the BPMN Event-based Gateway element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF

