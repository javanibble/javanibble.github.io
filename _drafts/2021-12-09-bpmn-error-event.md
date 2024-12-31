---
layout: post
title: "BPMN Error Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, error event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Error Event article provides a detailed explanation of the error event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Error Event article focus on the definition and usage of the error event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the error event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the error event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is an Error Event?
> "An Error represents the content of an Error Event or the Fault of a failed Operation." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the Error Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Error Event</td><td></td><td><iconify-icon height=48px data-icon="bpmn:start-event-error"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-error"></iconify-icon></td><td></td><td></td><td><iconify-icon height=48px data-icon="bpmn:end-event-error"></iconify-icon></td></tr>
</table>

BPMN Notation: Error Event
{:.figcaption}

## BPMN Event Types
The following table contains a list of the different Error Event types, their descriptions and the BPMN notations:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Error Event Sub-Process Event (Interrupting) | Whenever the Event occurs, the associated process is terminated. A downstream token is then generated, which activates the next element of the event-sub-process connected to the Event. | <iconify-icon height=48px data-icon="bpmn:start-event-error"></iconify-icon> |
| Error Boundary Event (Interrupting) | Whenever the Event occurs, the associated Activity is terminated. A downstream token is then generated, which activates the next element of the process connected to the Event. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-error"></iconify-icon> |
| Error End Event | Whenever this event is reached, the event will raise an error and the process will end. | <iconify-icon height=48px data-icon="bpmn:end-event-error"></iconify-icon> |

{:.stretch-table}
BPMN Event Types: Error Events
{:.figcaption}


## BPMN Diagram
The following is an example of a BPMN Error Event within a diagram:

![BPMN Error Event](/assets/images/posts/bpmn-error-event/bpmn-error-event.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Error Event
{:.figcaption}


## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Error Event as per the official
rules of the BPMN Specification.

* A catch Intermediate Error Event can only be attached to the boundary of an Activity and MAY NOT be used in normal flow.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* An Error Catch Events should have a Text Annotation with the `Error Code: {Error Code}` associated with it.
* An Error Throw Event should have a Text Annotation with the `Error Code: {Error Code}` associated with it.

## Finally
This article provided a detailed explanation of the BPMN Error Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF
