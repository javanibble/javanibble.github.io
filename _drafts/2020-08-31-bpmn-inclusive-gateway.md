---
layout: post
title: "BPMN Inclusive Gateway"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, inclusive gateway]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Inclusive Gateway article provides a detailed explanation of the inclusive gateway element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Inclusive Gateway article focus on the definition and usage of the inclusive gateway element as documented in the
BPMN 2.0 specification. The example process diagram illustrates the correct use of the inclusive gateway. The BPMN
Guidelines section contains a detailed set of rules that apply to the inclusive gateway and explains how the element may
or may not be used within the different BPMN diagrams.

## What is an Inclusive Gateway?
> "A diverging Inclusive Gateway (Inclusive Decision) can be used to create alternative but also parallel paths within a 
> process flow. A default path can optionally be identified, to be taken in the event that none of the conditional 
> expressions evaluate to true. A converging Inclusive Gateway is used to merge a combination of alternative and 
> parallel paths. A control flow token arriving at an Inclusive Gateway MAY be synchronized with some other tokens that 
> arrive later at this Gateway." ~ [BPMN Specification][1]

## Example: Order Coffee Process
The Place Order process illustrates the use of the inclusive gateway to make a decision based on the outcome of a task.
The process starts of with a task to place an order. Based on the outcome of this task, the process determines whether
the customer "Ordered Coffee" or "Ordered Muffin" or both. If no decision was made, the default task to give a free 
sample is performed. After the order is fulfilled, the final task to deliver the coffee order is performed. 

![Inclusive Gateway Example](/assets/images/posts/bpmn-inclusive-gateway/bpmn-inclusive-gateway.png){:.lead width="800" height="100" loading="lazy"}
Example of an inclusive gateway
{:.figcaption}

The converging inclusive gateway merges the sequence flows from the different tasks based on the choice of order. The incoming sequence flow tokens will be synchronised first (waiting on other tokens), before being routed to the outgoing sequence flow.

**Key Difference**
* Exclusive Gateway: A maximum of one sequence flow may be traversed by a token.
* Inclusive Gateway: More than one sequence flow may be traversed by a token 

## Guidelines
* The inclusive gateway is also referred to as OR.
* Each of the sequence flow's condition expression are evaluated.
* The true evaluation of one condition Expression does not exclude the evaluation of other condition Expressions. 
* All Sequence Flows with a true evaluation will be traversed by a token. 
* Since each path is considered to be independent, all combinations of the paths MAY be taken, from zero to all.
* Inclusive Gateways should be designed that at least one path is taken to avoid runtime exceptions. (See Default Path)
* The default flow will be used only if all the other outgoing conditional flow is not true at runtime.
* The default Sequence Flow should not have a conditionExpression. 

## Finally
This article provided a detailed explanation of the BPMN Inclusive Gateway element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/) 

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF