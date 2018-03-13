## Microservices-demo

1. [Sock-shop Application - Microservices demo](Sock-shop-microservices-demo.md)
2. [Istio를 이용한 Application Routing and discovery](Istio-side-car.md)
3. CQRS, Saga 

### Microservices Patterns 
by Chris Richardson

[![Microservices Patterns](./img/MicroservicePatternLanguage.jpg)](http://microservices.io/patterns/index.html)
  - Core Pattern
  - Decomposition
    - decompose by business capability 
    - decompose by subdomain
  - Deployment Pattern
    - **Service instance per Container**
    - Serverless deployment
    - Multiple service instances per host
    - Service instance per Host / VM
    - Service deployment Platform
  - Cross Cutting concerns : externalized configuration, logging, health checks, metrics, service registration and discovery, circuit breakers
  - Communication Patterns
    - Style
    - External API
      - API Gateway
      - Backend for front-end
    - Reliability
    - Service Discovery
      - Client-side discovery
      - Server-side discovery
      - Service Registry
      - Self Registry
      - 3rd party registration 
  - Data Managment
    - Database per service
    - Shared database
    - **Saga :Maintaining data consistency**
    - **CQRS**
    - API Composition
    - **Event Sourcing**
    - **Transaction log tailing**
    - Database triggers
    - Application Events
  - Security
    - Access Token
  - Testing
    - Service Component test
    - Service Integration Contract test
  - Obserability
    - Log Aggregation
    - Application metrics
    - Audit logging
    - Distributed tracing
    - Exception Tracking
    - Health check API
  - UI Patterns
    - Server-side page fragment composition
    - Cient-side composition

[출처 : http://microservices.io]
