---
layout: post
title: "BPMN 2.0 Diagrams"
author: andre
categories: [ software-engineering, business-process-automation ]
tags: [bpmn]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: Overview of BPMN 2.0 diagram types and their roles in modeling business processes.
comments: true
---

- Table of Contents
{:toc .large-only}

BPMN 2.0 provides a structured way to model business processes and streamline communication. In this post, we explore 
the different diagram types and how they help in representing complex workflows and interactions.  

The BPMN 2.0 (Business Process Model and Notation) specification defines several types of diagrams to model business 
processes, with a focus on improving communication between technical and non-technical stakeholders. The main types of 
diagrams in BPMN 2.0 are:

## Process Diagram
### Private Process (Internal Business Process)
A Private Process (Internal Business Process) in BPMN 2.0 represents the detailed workflow within a single organisation 
or business unit, focusing on tasks, decisions, and flows managed internally. It only uses sequence flows to model the 
execution of activities, without exposing any interactions with external participants or entities. 

<img alt="BPMN Activity" src="/assets/images/posts/bpmn-fundamentals/private_business_process.png" width="100%"/>

* **Purpose**: A Private Process models the detailed workflow within a single organisation or business unit, focusing on how tasks, events, and decisions are executed internally. It is used to optimize and document internal processes without showing interactions with external entities.
* **Components**: Key components include activities (tasks and sub-processes), events (start, end, and intermediate), gateways (decision points), and sequence flows that define the process order. The process is often divided into pools (representing the organization) and lanes (representing internal departments or roles).
* **Use Case**: Used for modeling internal operations such as employee onboarding, order processing, or product development, helping organizations streamline and optimize workflows within their boundaries.

### Public Process (Abstract Process)
A Public Process represents the interactions between a Private Business Process and another process or participant. Only 
the activities involved in communication with external participants are included, while all other internal activities 
remain hidden. 

The public process displays the message flows and their sequence, showing only what is necessary for interaction with 
external entities, making it an abstract view of the private process for the outside world.

<img alt="BPMN Activity" src="/assets/images/posts/bpmn-fundamentals/public_process.png" width="100%"/>

* **Purpose**: A Public Process shows the interactions between an organization's internal business process and external participants or systems, focusing only on the communication points and message flows required for these interactions. It presents a simplified view of how the organization interacts with external entities, hiding internal process details.
* **Components**: It includes activities that are involved in external communication, message flows (representing information exchanges), and pools (representing the organization and external participants). Unlike a private process, the internal tasks and sequence flows are not shown, only the message exchange interactions.
* **Use Case**: Used to model the communication between an organization and its partners, customers, or suppliers, such as sending order confirmations to customers or receiving product updates from suppliers, without exposing internal workflows.

## Collaboration Diagram
A Collaboration Diagram in BPMN 2.0 illustrates how two or more business entities (represented by pools) interact by 
exchanging messages through defined message flows, while each entity manages its internal processes independently. It 
provides a high-level view of inter-organisational communication, focusing on how participants collaborate without detailing their internal workflows. 

<img alt="BPMN Activity" src="/assets/images/posts/bpmn-fundamentals/collaborative_process.png" width="100%"/>

* **Purpose**: To represent interactions between two or more participants (represented by pools) in different processes.
* **Components**: Multiple pools (which represent different entities or participants), message flows (to show communication between participants), and tasks/events within each pool.
* **Use Case**: Used to show how different business entities (like organisations or systems) interact and exchange messages.

## Conversation Diagram
A Conversation Diagram in BPMN 2.0 focuses on the high-level communication between business participants by grouping 
related message exchanges into conversations. It provides an abstract view of how different entities interact, 
highlighting key communication points without detailing the underlying processes or message flows.

<img alt="BPMN Activity" src="/assets/images/posts/bpmn-fundamentals/conversation.png" width="100%"/>

* **Purpose**: To show high-level communication (conversations) between business participants.
* **Components**: Conversation nodes (grouping multiple message exchanges), message flows, and pools (representing participants).
* **Use Case**: Often used to show a high-level overview of communication or collaboration between organizations without going into process details.

## Choreography Diagram
A Choreography Diagram in BPMN 2.0 models the interactions between participants by focusing on the sequence of messages 
exchanged, rather than the internal processes of each participant. It shows how participants collaborate step-by-step 
through message-based interactions, defining the order and conditions of these exchanges.

<img alt="BPMN Activity" src="/assets/images/posts/bpmn-fundamentals/choregraphy.png" width="100%"/>

* **Purpose**: To depict the interactions between participants, focusing on the sequence of messages exchanged without focusing on the internal process of any particular participant.
* **Components**: Choreography tasks (defining interactions), participants, and message flows.
* **Use Case**: Ideal for describing protocol-level or contract-based interactions where the focus is on message exchange between entities.

## Summary
In summary, BPMN 2.0 offers a comprehensive framework for modeling business processes, enabling organizations to clearly 
visualise workflows and interactions. 

By utilising various diagram types, businesses can enhance communication, improve understanding among stakeholders, and 
drive process optimization.

[1]:https://www.omg.org/spec/BPMN/2.0/PDF