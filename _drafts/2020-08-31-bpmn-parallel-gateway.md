---
layout: post
title: "BPMN Parallel Gateway"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, parallel gateway]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Parallel Gateway article provides a detailed explanation of the parallel gateway element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Parallel Gateway article focus on the definition and usage of the parallel gateway element as documented in the
BPMN 2.0 specification. The example process diagram illustrates the correct use of the parallel gateway. The BPMN
Guidelines section contains a detailed set of rules that apply to the parallel gateway and explains how the element may
or may not be used within the different BPMN diagrams.

## What is a Parallel Gateway?
> "A Parallel Gateway creates parallel paths without checking any conditions; each outgoing Sequence Flow receives a 
> token upon execution of this Gateway. For incoming flows, the Parallel Gateway will wait for all incoming flows before 
> triggering the flow through its outgoing Sequence Flows." ~ [BPMN Specification][1]

## Example: Order Coffee Process
The Order Coffee process illustrates the use of the parallel gateway to perform two tasks in parallel. The process starts of with a task to *Retrieve Coffee Order*. The Parallel Gateway creates parallel paths (forks) without checking any conditions so that the *Make Coffee* and *Retrieve Cup & Saucer* tasks are performed in parallel. The parallel gateway (joins) waits for both tasks to complete, before finally moving on the *Pour Coffee in Cup* task. Once the *Deliver Coffee Order* task is complete, the process also finishes.

![Parallel Gateway Example](/assets/images/posts/bpmn-parallel-gateway/bpmn-parallel-gateway.png){:.lead width="800" height="100" loading="lazy"}
Example of an parallel gateway
{:.figcaption}

BPMN uses the term **fork** to refer to the dividing of a path into two or more parallel paths (also known as an AND-Split). It is a place in the Process where activities can be performed concurrently, rather than sequentially. BPMN uses the term **join** to refer to the combining of two or more parallel paths into one path (also known as an AND-Join or synchronization).

## Guidelines
* The parallel gateway is also referred to as AND-Split and AND-Join.
* The fact that tasks are modelled in parallel, does not mean they are processed in parallel.
* Modelling tasks in parallel, improves the process optimisation.
* The process instance is active as long as a one of the multiple tokens are active.

## Finally
This article provided a detailed explanation of the BPMN Parallel Gateway element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/) 

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF