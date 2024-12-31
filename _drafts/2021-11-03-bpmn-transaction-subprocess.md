---
layout: post
title: "BPMN Transaction Subprocess"
author: andre
categories: [ bpmn ]
tags: [bpmn, bpmn 2.0, transaction subprocess]
image: /assets/images/feature-images/feature-image-bpmn-fundamentals.jpg
description: "The BPMN Transaction Subprocess article provides a detailed explanation of the transaction subprocess element, including the BPMN notation, an example diagram and guidelines."
comments: true
related_posts:
- bpmn/_posts/2020-08-29-bpmn-diagrams.md
- bpmn/_posts/2020-08-30-bpmn-elements.md
---

- Table of Contents
{:toc .large-only}

The BPMN Transaction Subprocess article focus on the definition and usage of the transaction subprocess element as documented
in the BPMN 2.0 specification. The example process diagram illustrates the correct use of the transaction subprocess. The
BPMN Guidelines section contains a detailed set of rules that apply to the transaction subprocess and explains how the
element may or may not be used within the different BPMN diagrams.

## What is a Transaction Subprocess?
> "A Transaction is a specialized type of Sub-Process that will have a special behavior that is controlled through a 
> transaction protocol." ~ [BPMN Specification][1]


## BPMN Notation
The BPMN specification defines the Transaction Subprocess using the following description and notation:

| Element | Description | Notation |
|---------|-------------|:--------:|
| Transaction Subprocess | A Transaction is a specialized type of Sub-Process that will have a special behavior that is controlled through a transaction protocol. There are three basic outcomes of a Transaction: Successful completion, Failed completion & Hazard. | <iconify-icon height=48px data-icon="bpmn:transaction"></iconify-icon> |
{:.stretch-table}
BPMN Notation: Transaction Subprocess
{:.figcaption}

## Finally
This article provided a detailed explanation of the BPMN Transaction Subprocess element. Follow me on any of the different
social media platforms, and feel free to leave comments.

## Reference
* Business Process Model and Notation Specification Version 2.0.2. (2014, January). [https://www.omg.org/spec/BPMN/2.0.2/](https://www.omg.org/spec/BPMN/2.0.2/)

[1]:https://www.omg.org/spec/BPMN/2.0.2/PDF