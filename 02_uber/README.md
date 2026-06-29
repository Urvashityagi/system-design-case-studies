# Uber System Design (High-Level Design)

## Problem Statement

Design a scalable Uber-like ride-hailing system supporting millions of users with real-time driver tracking, ride matching, and dynamic pricing.

---

## Functional Requirements

- Rider can request a ride.
- Find nearby drivers.
- Real-time GPS updates.
- Ride matching.
- Surge pricing.
- Ride status tracking.
- Payment after ride completion.

---

## Non-Functional Requirements

- High Availability
- Low Latency
- Scalability
- Fault Tolerance
- Real-Time Processing

---

## High-Level Architecture

![Architecture](diagrams/uber-architecture.png)

### Components

- User
- Load Balancer
- API Gateway
- Ride Service
- Driver Service
- Location Service
- Redis (Nearby Drivers)
- Kafka
- Ride Matching Service
- Surge Pricing Service
- Notification Service
- MySQL
- Google Maps API

---

## Database Design

![Database](diagrams/Uber_db.png)

---

## Request Flow

1. Rider requests a ride.
2. API Gateway forwards the request to Ride Service.
3. Location Service finds nearby drivers using Redis GeoSpatial search.
4. Ride Matching Service selects the nearest available driver.
5. Driver accepts the ride.
6. Notifications are sent to rider and driver.
7. GPS updates are continuously published through Kafka.
8. Ride details and payment information are stored in MySQL.

---

## Scaling Strategy

- Horizontal scaling of all stateless services.
- Redis Cluster for location search.
- Kafka partitions with consumer groups.
- MySQL Read Replicas.
- Load Balancer distributes incoming traffic.

---

## Failure Handling

- Redis failure → Fallback to database (higher latency).
- Kafka failure → Use Outbox Pattern.
- Ride Matching failure → Kafka retries processing.
- Google Maps API failure → Retry and use cached routes if available.

---

## Trade-offs

- Redis provides fast nearby-driver search but increases infrastructure complexity.
- Kafka enables asynchronous processing with eventual consistency.
- Microservices improve scalability but add operational complexity.

---

## Technologies

- Spring Boot
- Kafka
- Redis
- MySQL
- REST APIs
- Docker
- Kubernetes
- Google Maps API