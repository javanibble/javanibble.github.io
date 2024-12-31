---
layout: post
title: "BPMN Signal Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, signal event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Signal Event article provides a detailed explanation of the signal event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Signal Event article focus on the definition and usage of the signal event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the signal event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the signal event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Signal Event?
> "The Signal Event differs from an Error Event in that the Signal defines a more general, non-error condition for 
> interrupting Activities (such as the successful completion of another Activity) as well as having a larger scope than 
> Error Events" ~ [BPMN Specification][1]

## BPMN Notation
The BPMN specification defines the Signal Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Signal Event</td><td><iconify-icon height=48px data-icon="bpmn:start-event-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-throw-signal"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:end-event-signal"></iconify-icon></td></tr>
</table>

BPMN Notation: Signal Event
{:.figcaption}

## Finally
This article provided a detailed explanation of the BPMN Signal Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF