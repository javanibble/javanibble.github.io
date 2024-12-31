---
layout: post
title: "BPMN 2.0 Guidelines"
author: andre
categories: [ BPMN ]
tags: [bpmn 2.0, bpmn guidelines]
image: assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Guidelines ..."
comments: true
related_posts:
- bpmn/_posts/2020-01-01-bpmn-ultimate-reference.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

  
This article describes the BPMN 2.0 guidelines ...


## Flow Objects
Flow Objects are the main graphical elements to define the behavior of a business process. There are three Flow Objects:

| Element | Description | Notation |
|---------|-------------|:--------:|
| [Event](#event) | An Event is something that “happens” during the course of a Process. These Events affect the flow of the model and usually have a cause (trigger) or an impact (result). There are three types of Events, based on when they affect the flow: Start, Intermediate, and End. | <iconify-icon height=48px data-icon="bpmn:start-event"></iconify-icon> |
| [Activity](#activity) | An Activity is a generic term for work that company performs in a Process. An Activity can be atomic or non-atomic (compound). The types of Activities that are a part of a Process Model are: Sub-Process and Task, which are rounded rectangles. | <iconify-icon height=48px data-icon="bpmn:task"></iconify-icon> |
| [Gateway](#gateway) | A Gateway is used to control the divergence and convergence of Sequence Flows in a Process. Thus, it will determine branching, forking, merging, and joining of paths. Internal markers will indicate the type of behavior control. | <iconify-icon height=48px data-icon="bpmn:gateway"></iconify-icon> |  
{:.stretch-table}

### Event

### Activity

### Gateway



## Data
Activities and processes often need data in order to execute. Data is represented with the four elements:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Data Object | Data Objects provide information about what Activities require to be performed and/or what they produce, Data Objects can represent a singular object or a collection of objects. | <iconify-icon height=48px data-icon="bpmn:data-object"></iconify-icon> |
| Data Inputs | Data requirements are captured as Data Inputs. | <iconify-icon height=48px data-icon="bpmn:data-input"></iconify-icon> |
| Data Outputs | Data that is produced is captured using Data Outputs. | <iconify-icon height=48px data-icon="bpmn:data-output"></iconify-icon> |
| Data Stores | A DataStore provides a mechanism for Activities to retrieve or update stored information that will persist beyond the scope of the Process. | <iconify-icon height=48px data-icon="bpmn:data-store"></iconify-icon> |
{:.stretch-table}

## Connecting Objects
There are multiple ways of connecting the Flow Objects to each other or other information.

| Element | Description | Notation |
|---------|-------------|:--------:|
| [Sequence Flow](#sequence-flow) | A Sequence Flow is used to show the order that Activities will be performed in a Process. | <iconify-icon height=48px data-icon="bpmn:connection"></iconify-icon> |
| [Message Flow](#message-flow) | A Message Flow is used to show the flow of Messages between two Participants that are prepared to send and receive them. |  |
| Association | An Association is used to link information and Artifacts with BPMN graphical elements. Text Annotations and other Artifacts can be Associated with the graphical elements. The same as an association except, an arrowhead on the Association indicates a direction of flow (e.g., data), when appropriate. |  |
{:.stretch-table}


### Message Flow


## Swimlanes
There are two ways of grouping the primary modeling elements through Swimlanes:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Pool | A Pool is the graphical representation of a Participant in a Collaboration. It also acts as a “swimlane” and a graphical container for partitioning a set of Activities from other Pools. A Pool MAY have internal details, in the form of the Process that will be executed. Or a Pool MAY have no internal details, i.e., it can be a "black box." | <iconify-icon height=48px data-icon="bpmn:participant"></iconify-icon> |
| Lane | A Lane is a sub-partition within a Process, sometimes within a Pool, and will extend the entire length of the Process, either vertically or horizontally. Lanes are used to organize and categorize Activities. | <iconify-icon height=48px data-icon="bpmn:lane-divide-two"></iconify-icon> |
{:.stretch-table}

## Artifacts
Artifacts are used to provide additional information about the Process. The current set of Artifacts includes:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Group | A Group is a grouping of graphical elements that are within the same Category. This type of grouping does not affect the Sequence Flows within the Group. The Category name appears on the diagram as the group label. | <iconify-icon height=48px data-icon="bpmn:group"></iconify-icon> |
| Text Annotation | Text Annotations are a mechanism for a modeler to provide additional text information for the reader of a BPMN Diagram. | <iconify-icon height=48px data-icon="bpmn:text-annotation"></iconify-icon> |
{:.stretch-table}


## Guidelines

### Activity Guidelines
* An Activity MAY be the target of a Message Flow; it can have zero (0) or more incoming Message Flows.
* An Activity MAY be a source of a Message Flow; it can have zero (0) or more outgoing Message Flows.

### Sequence Flow Guidelines
* An Artifact MUST NOT be a target for a Sequence Flow.
* An Artifact MUST NOT be a source for a Sequence Flow. 
* An Event Sub-Process MUST NOT have any incoming or outgoing Sequence Flows. 
* A Start Event MUST NOT be a target for Sequence Flows; it MUST NOT have incoming Sequence Flows.

### Message Flow Guidelines

* A Message Flow MUST connect two separate Pools
* A Message Flow MUST either connect to the Pool boundary or to Flow Objects within the Pool boundary.
* A Message Flow MUST NOT connect two objects within the same Pool.
  
* An Artifact MUST NOT be a target for a Message Flow.
* An Artifact MUST NOT be a source for a Message Flow.

* An Activity MAY be the target of a Message Flow; it can have zero (0) or more incoming Message Flows.
* An Activity MAY be a source of a Message Flow; it can have zero (0) or more outgoing Message Flows.

* A Start Event MAY be the target for a Message Flow; it can have zero (0) or more incoming Message Flows. 
* A Start Event MUST NOT be a source for a Message Flow; it MUST NOT have outgoing Message Flows.



### Event Sub-Process
* An Event Sub-Process MUST NOT have any incoming or outgoing Sequence Flows.

### Start Event
* A Start Event MUST NOT be a target for Sequence Flows; it MUST NOT have incoming Sequence Flows.
* A Start Event MAY be the target for a Message Flow; it can have zero (0) or more incoming Message Flows.
* A Start Event MUST NOT be a source for a Message Flow; it MUST NOT have outgoing Message Flows.

### Artifact Guidelines
* An Artifact MUST NOT be a target for a Sequence Flow.
* An Artifact MUST NOT be a source for a Sequence Flow.
* An Artifact MUST NOT be a target for a Message Flow.
* An Artifact MUST NOT be a source for a Message Flow.

## Summary
Congratulations! You have finished the post about BPMN 2.0 Guidelines. Follow me on any of the different social media platforms and feel free to leave comments.


## Facts
### Start Event
A Start Event generates a token that MUST eventually be consumed at an End Event (which MAY be implicit if not
graphically displayed). The path of tokens should be traceable through the network of Sequence Flows, Gateways, and
Activities within a Process.

### Message Flows
Each Message Flow targeting a Start Event represents an instantiation mechanism (a trigger) for the Process. Only one of the triggers is REQUIRED to start a new Process.

A token does not traverse a Message Flow since it is a Message that is passed down a Message Flow (as the name implies).