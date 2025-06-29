# API Gateway

The `api-gateway` module acts as a centralized entry point for all microservices in the architecture. It is built using **Spring Cloud Gateway** and leverages **Eureka Service Discovery** to route requests dynamically to registered services.

## Features

- **Dynamic Routing via Eureka**
- **Path-based Routing**
- **Prefix Stripping**
- **Load Balancing (via Ribbon under the hood)**
- **Service Discovery Integration**
- Ready for integration with:
  - CORS
  - Authentication / Authorization
  - Rate Limiting
  - Logging / Tracing

## Technologies

- **Java 17+**
- **Spring Boot 3**
- **Spring Cloud Gateway**
- **Spring Cloud Netflix Eureka Client**

---

## Configuration Overview

### `application.yml`

Right now the service is configured to use automatic routing, then it is not necessary to configure the routes manually like this example, but it is another way to configurate the routing.
```yaml
server:
  port: 8765

spring:
  application:
    name: api-gateway

  cloud:
    gateway:
      discovery:
        locator:
          enabled: false
      routes:
        - id: products-api
          uri: lb://products_api
          predicates:
            - Path=/products-api/**
          filters:
            - StripPrefix=1

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

## Key Notes
lb://products_api: Routes traffic to the products_api service registered in Eureka.

StripPrefix=1: Removes /products-api from the URI before forwarding to the service.

Runs on port 8765.

Eureka should be running at http://localhost:8761.

### Example of routing

- Incoming Request: GET http://localhost:8765/products-api/v1/products
- Routed to: products_api -> GET /v1/products
