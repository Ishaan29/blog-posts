# Mastering API Rate Limiter Design: A Comprehensive Guide for System Design Interviews

## Introduction

An API rate limiter is a crucial component of any API infrastructure that helps control and manage incoming requests from clients or third-party applications. By imposing limits on the number of requests an API can handle within a specific time frame, rate limiters prevent abuse, protect against DDoS attacks, and maintain a fair distribution of resources among users.

### Why does this question come up so frequently in System Design Interviews?

It assesses a candidate's understanding of scalability, security, performance optimization, system architecture, API best practices, and real-time monitoring within a single evaluation criterion.

## Requirements Gathering

It is always beneficial to ask clarifying questions to gain a better understanding of the system's scope. In the context of designing an API rate limiter, some relevant questions include:

- Should the API rate limiter be implemented on the client side or the service side?
- What types of throttle rules should our system support?
- What scale of traffic should the system be capable of handling, considering orders of magnitude?
- Is it necessary to notify users when their requests are being throttled?

Once a sufficient understanding of the system is obtained, we can proceed with defining both functional and non-functional requirements.

### Functional Requirements

For the article's scope, the chosen standard requirements include:

- Rate limiter should be flexible enough to support different sets of throttling rules.
- Should be able to handle large traffic.
- Should be deployed in a distributed environment.
- The system should show a message saying that their request has been throttled.

### Non-Functional Requirements

- **Performance:** The rate limiter should have minimal impact on the overall system performance and response times.
- **Scalability:** Designed to scale horizontally.
- **Reliability:** Highly reliable, with built-in fault tolerance.
- **Configuration and Management:** User-friendly interface for configuring and managing the throttling rules.
- **Monitoring and Analytics:** Comprehensive capabilities for tracking and analyzing usage patterns.

## Design Scope

We will focus on designing a server-side API rate limiter, which offers enhanced security compared to a client-side limiter. Implementing the rate limiter as a standalone service allows for optimized resource utilization and compatibility with diverse API server environments.

## Algorithms for Rate Limiting

### Token Bucket

A popular technique that controls the rate of incoming requests by using a metaphorical bucket that holds a fixed number of tokens.

### Leaking Bucket

Controls the flow of requests by using a metaphorical bucket that has a leak, ensuring a consistent outflow of requests.

### Fixed Window Counter

Counts the number of requests within a fixed time window to control the rate of incoming requests.

### Sliding Window Log

Uses a sliding time window to control the rate of incoming requests with a more granular approach.

### Sliding Window Counter

Tracks the number of requests within a sliding time window to control the rate of incoming requests.

## Design

### How are rate limiting rules created? Where are the rules stored?

### How to handle requests that are rate limited?

Let's take a look at how some industry-standard rate limiters define their rules:

```yaml
domain: messages
descriptor:
  key: message_type
  value: marketing
  rate_limit:
    unit: day
    requests_per_unit: 5
domain: auth
descriptor:
  key: auth_type
  value: login
  rate_limit:
    unit: min
    requests_per_unit: 3

