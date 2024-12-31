---
layout: post
title: "Cheat Sheet - Terminal"
date: 2020-01-02 00:00:00 +0200
tags: cheatsheet terminal commands macOS
categories: [Cheat sheet]
author: "andre_mare"
post_image: "/assets/img/my_images/cheat-sheets/cheatsheet-terminal.png"
---

The

#### 1. Maven Dependency
To add Spring Boot Actuator to your application, add the `spring-boot-starter-actuator` dependency to your Maven project.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>
```

#### 2. Actuator Endpoints
The Spring Boot Actuator endpoints are all disabled by default except for /health and /info.

*Enabling Endpoints*

All endpoints are enabled by default except for `shutdown`. To enable or disable any endpoint, you can use the 
`management.endpoint.<id>.enabled` property. Set the  `management.endpoints.enabled-by-default` property to `false` to 
disable all endpoints by default and set the individual endpoints that you would like to enable. 

```properties
# Enable the shutdown endpoint
management.endpoint.shutdown.enabled=true

# Disbale the bean endpoint
management.endpoint.bean.enabled=false

# Disable all the endpoints by default
management.endpoints.enabled-by-default=false
``` 

*Exposing Endpoints*

To change which endpoints are exposed, use the following technology-specific include and exclude properties:

```properties
# Exclude the endpoints exposed by JMX
management.endpoints.jmx.exposure.exclude=shutdown,bean

# Include the endpoints exposed by JMX (Default *) 
management.endpoints.jmx.exposure.include=env

# Exclude the endpoints exposed by Web
management.endpoints.web.exposure.exclude=

# Include the endpoints exposed by Web (Default info, health)
management.endpoints.web.exposure.include=info, health, env
```


| ID | Description| Enabled | Exposed JMX | Exposed Web | Path |
|---|---|---|---|---|---|
| `auditevents` | . | Yes | Yes | No | /actuator/auditevents |
| `beans` | . | Yes | Yes | No | /actuator/beans |
| `caches`| . | Yes | Yes | No | /actuator/caches |
| `conditions`| . | Yes |Yes | No | /actuator/conditions |
| `configprops`| . | Yes | Yes | No | /actuator/configprops |
| `env`| . | Yes | Yes | No | /actuator/env |
| `flyway`| . | Yes | Yes | No | /actuator/flyway |
| `health`| . | Yes | Yes | Yes | /actuator/health |
| `heapdump`| . | Yes | N/A | Yes | /actuator/heapdump |
| `httptrace`| . | Yes | Yes | No | /actuator/httptrace |
| `info`| . | Yes | Yes | Yes | /actuator/info |
| `integrationgraph`| . | Yes | Yes | No | /actuator/integrationgraph |
| `jolokia`| . | Yes | N/A | No | /actuator/jolokia |
| `logfile`| . | Yes | N/A | No | /actuator/logfile |
| `loggers`| . | Yes | Yes | No | /actuator/loggers |
| `liquibase`| . | Yes | Yes | No | /actuator/liquibase |
| `metrics`| . | Yes | Yes | No | /actuator/metrics |
| `mappings`| . | Yes | Yes | No | /actuator/mappings |
| `prometheus`| . | Yes | N/A | No | /actuator/prometheus |
| `scheduledtasks`| . | Yes | Yes | No | /actuator/scheduledtasks |
| `sessions`| . | Yes | Yes | No | /actuator/sessions |
| `shutdown`| . | No | Yes | No | /actuator/shutdown |
| `threaddump`| . | Yes | Yes | No | /actuator/threaddump |

#### 
* [Spring Documentation: Spring Boot Actuator](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html)
* [Baeldung: Spring Boot Actuator](https://www.baeldung.com/spring-boot-actuators)
* [Udemy: Ready for production with Spring Boot Actuator](https://www.udemy.com/course/ready-for-production-with-spring-boot-actuator/)

#### References
