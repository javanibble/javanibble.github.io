---
layout: post
title: "BPMN Exclusive Gateway"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, exclusive gateway]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Exclusive Gateway article provides a detailed explanation of the exclusive gateway element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Exclusive Gateway article focus on the definition and usage of the exclusive gateway element as documented in the
BPMN 2.0 specification. The example process diagram illustrates the correct use of the exclusive gateway. The BPMN
Guidelines section contains a detailed set of rules that apply to the exclusive gateway and explains how the element may
or may not be used within the different BPMN diagrams. 

## What is an Exclusive Gateway?
> "A diverging Exclusive Gateway (Decision) is used to create alternative paths within a Process flow. This is basically 
> the “diversion point in the road” for a Process. For a given instance of the Process, only one of the paths can be 
> taken.
>
>A converging Exclusive Gateway is used to merge alternative paths. Each incoming Sequence Flow token is routed to the 
> outgoing Sequence Flow without synchronization." ~ [BPMN Specification][1]

## Example: Order Coffee Process
The Order Coffee process illustrates the use of the exclusive gateway to make a decision based on the outcome of a task.
The process starts of with a task to retrieve the coffee order. Based on the outcome of this task, a decision is made 
whether to make "Espresso" or "Caffe Mocha". If no decision was made, the default task to give a free sample is 
performed. After the beverage is made, the final task to deliver the coffee order is performed. 

![Exclusive Gateway Example](/assets/images/posts/bpmn-exclusive-gateway/bpmn-exclusive-gateway.png){:.lead width="800" height="100" loading="lazy"}
Example of an exclusive gateway
{:.figcaption}

The diverging exclusive gateway in the above example makes a decision based on the question "Choice of Coffee?". The 
question has a predefined set of alternative answers. Each answer, "Espresso", "Caffe Mocha" and "Default" is associated
with a condition expression that is associated with the gateway’s outgoing sequence flows.

The converging exclusive gateway merges the sequence flows from the different tasks based on the choice of coffee. The 
incoming sequence flow tokens will be routed to the outgoing sequence flow without synchronisation (waiting on other tokens).

**Key Difference**
* Exclusive Gateway: A maximum of one sequence flow may be traversed by a token.
* Inclusive Gateway: More than one sequence flow may be traversed by a token 

## Guidelines
* The exclusive gateway is also referred to as XOR.
* The exclusive gateway may use an "X" marker within the gateway diamond. This marker is **optional**.
* The use of the "X" marker should be consistently applied or left out in the process diagram.  
* The default flow will be used only if all the other outgoing conditional flow is not true at runtime.
* The default Sequence Flow should not have a conditionExpression. 
* The use of a converging exclusive gateway is optional. The multiple sequence flows may be directly connected to next 
activity, event, or another gateway.


## Finally
This article provided a detailed explanation of the BPMN Exclusive Gateway element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF