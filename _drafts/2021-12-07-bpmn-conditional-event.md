---
layout: post
title: "BPMN Conditional Event"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, conditional event]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Conditional Event article provides a detailed explanation of the conditional event element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Conditional Event article focus on the definition and usage of the conditional event element as documented in the BPMN 2.0
specification. The example process diagram illustrates the correct use of the conditional event annotation. The BPMN Guidelines
section contains a detailed set of rules that apply to the conditional event and explains how the element may or may not be used
within the different BPMN diagrams.

## What is a Conditional Event?
> "Conditional triggers are implicitly thrown. When they are activated they wait for a status based condition respectively to trigger the catch Event. This type of event is triggered when a condition become true." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the Conditional Event element using the following description and notation:

<table class="stretch-table" style="text-align: center;" border="1">
<tr><td rowspan="3"></td><td colspan="6" align="center">Catching Events</td><td colspan="2">Throwing Events</td></tr>
<tr><td colspan="3" align="center">Start Event</td><td colspan="4">Intermediate Event</td><td>End Event</td></tr>
<tr><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-lr; transform: rotate(180deg);">Standard</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Event Sub-Process <br> Non-Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Catching</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary <br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-rl;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Boundary Non-<br> Interrupting</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Throwing</SPAN></td><td><SPAN STYLE="writing-mode: vertical-lr;-ms-writing-mode: tb-rl; transform: rotate(180deg);">Standard</SPAN></td></tr>
<tr><td style="text-align: left;">Conditional Event</td><td><iconify-icon height=48px data-icon="bpmn:start-event-condition"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-condition"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-condition"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-condition"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-condition"></iconify-icon></td><td><iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-condition"></iconify-icon></td><td></td><td></td></tr>
</table>

BPMN Notation: Conditional Event
{:.figcaption}

## BPMN Event Types
The following table contains a list of the different Conditional Event types, their descriptions and the BPMN notations:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Conditional Start Event | This type of Event is triggered when a condition (a type of Expression) becomes true. Whenever the Event occurs, a new process instance is started. | <iconify-icon height=48px data-icon="bpmn:start-event-condition"></iconify-icon> |
| Conditional Event Sub-Process Event (Interrupting) | This type of Event is triggered when a condition (a type of Expression) becomes true. Whenever the Event occurs, execution of the enclosing Sub-Process is cancelled and the Event Sub-Process continues execution. | <iconify-icon height=48px data-icon="bpmn:start-event-condition"></iconify-icon> |
| Conditional Event Sub-process Event (Non-Interrupting) | This type of Event is triggered when a condition (a type of Expression) becomes true. Whenever the Event occurs, execution of the enclosing Sub-Process continues in parallel to the Event Sub-Process. | <iconify-icon height=48px data-icon="bpmn:start-event-non-interrupting-condition"></iconify-icon> |
| Conditional Intermediate Catch Event | This type of Event is triggered when a condition (a type of Expression) becomes true. Whenever the Event occurs, the event allows the process to continue. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-condition"></iconify-icon> |
| Conditional Boundary Event (Interrupting) | This type of Event is triggered when a condition (a type of Expression) becomes true. Whenever the event occurs, the associated Activity is terminated. A downstream token is then generated, which activates the next element of the Process. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-condition"></iconify-icon> |
| Conditional Boundary Event (Non-Interrupting) | This type of Event is triggered when a condition (a type of Expression) becomes true. Whenever the Event occurs, the associated Activity continues to be active. As a token is generated for the Sequence Flow from the boundary Event in parallel to the continuing execution of the Activity. | <iconify-icon height=48px data-icon="bpmn:intermediate-event-catch-non-interrupting-condition"></iconify-icon> |

{:.stretch-table}
BPMN Event Types: Conditional Events
{:.figcaption}


## BPMN Diagram
The following is an example of a BPMN Conditional Event within a diagram:

![BPMN Conditional Event](/assets/images/posts/bpmn-conditional-event/bpmn-conditional-event.png){:.lead width="800" height="100" loading="lazy"}
Example of BPMN Conditional Event
{:.figcaption}


## BPMN Standards & Guidelines
The difference between standard and guideline is that a standard is a level of quality or attainment while a guideline
is a non-specific rule or principle that provides direction to action or behaviour. A standard are high in authority and
needs to be adhered to versus a guideline is low in authority and guide one in setting standards or determining a course
of action.

### BPMN Standards
The BPMN Standards section contains a list of rules that are applicable to the BPMN Conditional Event as per the official
rules of the BPMN Specification.

* The condition Expression for the Event MUST become false and then true before the Event can be triggered again.
* The condition Expression of a Conditional Start Event MUST NOT refer to the data context or instance attribute of the Process (as the Process instance has not yet been created).
* The condition Expression of a Conditional Start Event MAY refer to static Process attributes and states of entities in the environment.

### BPMN Guidelines
The BPMN guidelines section contains a list of optional rules that can be used as a guide.

* A Conditional Start Event should have a Text Annotation describing the condition that would trigger the event.

## Finally
This article provided a detailed explanation of the BPMN Conditional Event element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF



