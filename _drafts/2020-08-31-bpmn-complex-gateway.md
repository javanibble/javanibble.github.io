---
layout: post
title: "BPMN Complex Gateway"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, complex gateway]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Complex Gateway article provides a detailed explanation of the complex gateway element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Complex Gateway article focus on the definition and usage of the complex gateway element as documented in the 
BPMN 2.0 specification. The example process diagram illustrates the correct use of the complex gateway. The BPMN 
Guidelines section contains a detailed set of rules that apply to the complex gateway and explains how the element may 
or may not be used within the different BPMN diagrams.

## What is a Complex Gateway?
> "The Complex Gateway can be used to model complex synchronization behavior. An expression activationCondition is used 
> to describe the precise behavior. For example, this expression could specify that tokens on three out of five incoming 
> Sequence Flows are needed to activate the gateway. What tokens are produced by the gateway is determined by conditions 
> on the outgoing Sequence Flows as in the split behavior of the Inclusive Gateway. If tokens arrive later on the two 
> remaining Sequence Flows, those tokens cause a reset of the gateway and new token can be produced on the outgoing 
> Sequence Flows. To determine whether it needs to wait for additional tokens before it can reset, the gateway uses the 
> synchronization semantics of the Inclusive Gateway." ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Complex Gateway element using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Complex Gateway | The BPMN modeller can use the Complex Gateway to model complex synchronization behaviour. | <iconify-icon height=48px icon="bpmn:gateway-complex"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Complex Gateway
{:.figcaption}

## BPMN Diagram
The following is an example of a BPMN Complex Gateway within a diagram:

![BPMN Complex Gateway](/assets/images/posts/bpmn-complex-gateway/bpmn-complex-gateway.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Complex Gateway
{:.figcaption}

The complex gateway implements unique merging behaviour. In the above diagram, the parallel gateway generates three 
tokens that flow toward the three individual activities: Step A, Step B, and Step C. The process diagram illustrates how
the complex gateway blocks the inbound tokens until the special condition is met. Only then will the token move on to 
activity (Step D).

The complex gateway as an element of convergence is used to continue to the next activity (Step D) only when a specific
business condition is met. The complex gateway as an element of divergence is used to control complex decision points.

## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN element.

* The Complex Gateway MUST use a marker that is in the shape of an asterisk and is placed within the Gateway diamond.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* The Complex Gateway requires a text annotation that describes the special merging behaviour.

## Finally
This article provided a detailed explanation of the BPMN Complex Gateway element. Follow me on any of the different 
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)
 
[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF