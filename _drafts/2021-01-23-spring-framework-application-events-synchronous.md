---
layout: post
title: "Spring Framework - Application Events (Synchronous)"
author: andre
categories: [ spring-boot ]
tags: [events, observer pattern, spring-boot, spring, java]
image: /assets/images/feature-images/feature-image-spring.jpg
description: This article explains the use of Application Events within the Spring framework to exchange information synchronously between loosely coupled components.
comments: true
---

- Table of Contents
{:toc .large-only}

Spring application events have been part of the Spring Framework from the beginning. The application events of the spring
framework is an implementation of the Observer pattern. The Observer pattern serves as a means to exchange information 
between loosely coupled components.

## Multi-part Series
This article forms part of a multi-part series on Spring Framework Application Events.

* [Spring Framework - Application Events (Synchronous)][Article1]


## Application Events - Synchronous 
The spring framework has an event mechanism that forms part of the `ApplicationContext`. The event publisher (subject) 
publishes an event, while the event listener (observer) only receives the specific event if the event listener listens 
for that specific type of event. 

The application event capability of the Spring framework is **synchronous** by default. This implies the publisher 
method blocks until all registered listeners have processed the event.  

### Application Event - MessageEvent
The `MessageEvent` is an application event and extends the `ApplicationEvent` abstract class. The `MessageEvent` class 
contains a String property called `message` that stores the event data.

The `ApplicationEvent` class is abstract since it doesn't make sense for generic events to be published directly.

```java
public class MessageEvent extends ApplicationEvent {

    private String message;

    public MessageEvent(final Object source, final String message) {
        super(source);
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}
```

**Javadoc**
* [ApplicationEvent](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationEvent.html)

### Event Publisher - SpringEventPublisher 
The `SpringEventPublisher` class creates an instance of a `MessageEvent` class. The `MessageEvent` is initialised with
the message that is the event data for the event listeners. The `MessageEvent` is also initialised with a reference to 
the current instance of the `SpringEventPublisher` class.

The `SpringEventPublisher` publish the `MessageEvent` which notifies all matching listeners registered with this 
application of an application event.

The publication of the event is effectively a hand-off to the multicaster and does not imply synchronous/asynchronous
execution or even immediate execution at all.
```java
@Component
public class SpringEventPublisher {

    private static final Logger logger = LoggerFactory.getLogger(SpringEventPublisher.class);

    @Autowired
    private ApplicationEventPublisher applicationEventPublisher;

    public void publishBasicEvent(final String message) {
        logger.info("SpringEventPublisher: Publish Event Started.");

        MessageEvent basicSpringEvent = new MessageEvent(this, message);
        applicationEventPublisher.publishEvent(basicSpringEvent);

        logger.info("SpringEventPublisher: Publish Event Complete.");
    }
}
```

**Javadoc**
* [ApplicationEventPublisher](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationEventPublisher.html)

### Event Listener - SynchronousEventListener
The `SynchronousEventListener` is an `ApplicationListener` that listens to for an event. The `ApplicationListener` is 
based on the standard `java.util.EventListener` interface for the Observer design pattern.

The `onApplicationEvent` handles the application event, which in this case is the `MessageEvent`. The Listener has 
access to the event data via the accessor method of the `message` property.
 
```java
@Component
public class SynchronousEventListener implements ApplicationListener<MessageEvent> {

    private static final Logger logger = LoggerFactory.getLogger(SynchronousEventListener.class);

    @Override
    public void onApplicationEvent(MessageEvent basicEvent) {
        logger.info("SynchronousEventListener: Receive Event: "+ basicEvent.getMessage());
    }
}
```

**Javadoc**
* [ApplicationListener](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationListener.html)

## Example Code
The source code used in this example can be found on [Github](https://github.com/javanibble/spring-events-example/tree/master/synchronous_events).

## Summary
This article explained the spring framework application event capability as an implementation of the Observer pattern. 
The application events of the spring framework are synchronous by default. The article also contains sample code for the
application event, the event publisher and the event listener.

Follow me on any of the different social media platforms and feel free to leave comments.

[Article1]:https://www.javanibble.com/spring-framework-application-events-synchronous/
