---
layout: post
title: "BPMN Parallel Multiple Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, parallel multiple event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Parallel Multiple Event article provides a detailed explanation of the parallel multiple event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Parallel Multiple Event article focus on the definition and usage of the parallel multiple event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the parallel multiple event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the parallel multiple event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Parallel Multiple Event?
> "This means that there are multiple triggers REQUIRED before the Process can be instantiated. All of the types of 
> triggers that are listed in the Start Event MUST be triggered before the Process is instantiated." ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Parallel Multiple Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Parallel Multiple Event</td><td><iconify-icon height=48px data-icon="bpmn:start-event-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-parallel-multiple"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-parallel-multiple"></iconify-icon></td><td></td><td></td></tr>
</table>

BPMN Notation: Parallel Multiple Event
{:.figcaption}

## Finally
This article provided a detailed explanation of the BPMN Parallel Multiple Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)


[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF