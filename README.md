# Eureka Server

## Overview

The **Eureka Server** acts as the Service Registry for the E-Learn Microservices Platform. It enables dynamic service discovery by allowing all microservices to register themselves automatically and discover other services without relying on hardcoded URLs.

By using Eureka, the platform achieves loose coupling, scalability, and high availability between microservices.

---

## Responsibilities

* Service Registration
* Service Discovery
* Service Health Monitoring
* Instance Management
* Dynamic Service Lookup
* Load Balancer Support
* Microservice Registry

---

## Technology Stack

* Java 17
* Spring Boot 3
* Spring Cloud Netflix Eureka Server
* Spring Boot Actuator

---

## Features

### Service Registry

All backend services register automatically with Eureka during startup.

Registered Services

* API Gateway
* User Service
* Course Service
* Purchase Service
* Review Service
* Notification Service

Future Services

* Analytics Service
* Search Service

---

### Service Discovery

Instead of using fixed URLs like:

```text
http://localhost:8081
```

Services communicate using logical names:

```text
lb://USER-SERVICE

lb://COURSE-SERVICE

lb://PURCHASE-SERVICE

lb://REVIEW-SERVICE
```

Spring Cloud LoadBalancer automatically resolves the service instance.

---

## Architecture

```text
                    Angular Frontend
                           │
                           ▼
                     API Gateway
                           │
                           ▼
                     Eureka Server
                           │
        ┌──────────┬──────────┬──────────┬──────────┐
        ▼          ▼          ▼          ▼          ▼
 User Service  Course Service Purchase  Review  Notification
                                   Service  Service   Service
```

---

## Service Registration Flow

```text
Microservice Starts
        │
        ▼
Registers with Eureka
        │
        ▼
Eureka Stores Instance
        │
        ▼
Other Services Discover It
        │
        ▼
Communication via Service Name
```

---

## Registered Services

| Service              | Purpose                             |
| -------------------- | ----------------------------------- |
| API Gateway          | Entry point for all client requests |
| User Service         | Authentication & User Management    |
| Course Service       | Course Management                   |
| Purchase Service     | Course Enrollment & Purchase        |
| Review Service       | Ratings & Reviews                   |
| Notification Service | Event-driven Notifications          |

---

## High-Level Request Flow

```text
Client Request
      │
      ▼
API Gateway
      │
      ▼
Eureka Server
      │
      ▼
Target Microservice
      │
      ▼
Business Logic
      │
      ▼
Response
```

---

## Configuration

The Eureka Server is configured to:

* Accept service registrations
* Maintain service registry
* Monitor instance health
* Remove inactive instances automatically
* Support dynamic service discovery

---

## Monitoring

Spring Boot Actuator endpoints are enabled.

Available endpoints

* `/actuator/health`
* `/actuator/info`
* `/actuator/prometheus`
* `/actuator/metrics`

---

## Benefits of Eureka

* No hardcoded service URLs
* Dynamic service registration
* Automatic service discovery
* Loose coupling between microservices
* Easier horizontal scaling
* Improved fault tolerance
* Simplified deployment

---

## Future Enhancements

* Eureka Cluster
* High Availability
* Multi-Region Service Discovery
* Secure Registration
* TLS/SSL Support
* Service Metadata
* Instance Tags
* Health Check Customization

---

## Project Structure

```text
eureka-server
│
├── config
├── resources
└── EurekaServerApplication.java
```

---

## Role in E-Learn Platform

The Eureka Server serves as the central service registry for the E-Learn Microservices Platform. It enables all backend services to register themselves dynamically and discover one another without relying on hardcoded network addresses. This simplifies communication between microservices and supports scalable, cloud-native deployments.

---

## Future Architecture

```text
                  Angular 18
                       │
                       ▼
                 API Gateway
                       │
                       ▼
                 Eureka Server
                       │
      ┌────────────────┼────────────────┐
      ▼                ▼                ▼
 User Service    Course Service   Purchase Service
      │                │                │
      ├────────────────┼────────────────┤
      ▼                ▼                ▼
 Review Service  Notification   Analytics Service
                       │
                       ▼
                    Apache Kafka
                       │
                       ▼
                Redis / MySQL
```

---

## Author

**Anil Mondi**

