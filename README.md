# 🌐 Centralized-Configuration-Server (Spring Cloud Config)

Hi, I built this project to gain a **clear and practical understanding of centralized configuration management in a microservices architecture** using **Spring Cloud Config Server**.

This project demonstrates how multiple microservices can **externalize their configuration**, store it in a **Git repository**, and fetch it dynamically from a **central Config Server**, following real-world enterprise practices.

<br>

The project is designed to help learners clearly understand:

- Why centralized configuration is needed in microservices  
- How Spring Cloud Config Server works  
- Git-based configuration management  
- Environment-specific configuration (dev / qa / prod)  
- Microservice startup configuration flow  

<br><br>

---

## Project Overview

This is a **Spring Boot–based Config Server application** that acts as a **single source of truth for all microservice configurations**.

Instead of storing configuration inside each microservice, all configurations are maintained in a **Git-backed repository**, and microservices fetch their configuration from the **Config Server** at startup.

The goal of this project is **hands-on learning of real-world microservices configuration management**.

<br>

---

## Why Centralized Configuration?

In microservices architecture:

- Each service runs independently  
- Configuration differs across environments  
- Managing configs inside services causes duplication  

Spring Cloud Config solves this by:

- Centralizing configuration  
- Version controlling configs using Git  
- Allowing services to be deployed once and configured dynamically  

<br>

---

## Technologies Used

<li>Java</li>
<li>Spring Boot</li>
<li>Spring Cloud Config Server</li>
<li>Spring Cloud Config Client</li>
<li>Spring Actuator</li>
<li>Git</li>
<li>REST APIs</li>
<li>Maven</li>

<br>

---

## What I Learned From This Project

<li>Importance of centralized configuration</li>
<li>Spring Cloud Config Server internals</li>
<li>Git-backed configuration management</li>
<li>Profile-based configuration loading</li>
<li>Difference between <code>bootstrap.yml</code> and <code>application.yml</code></li>
<li>Microservice startup configuration flow</li>
<li>Runtime configuration refresh using Actuator</li>
<li>Enterprise configuration best practices</li>

<br>

---

## Application Architecture

The project follows a **centralized configuration architecture**:

<li>Config Server – Central configuration provider</li>
<li>Git Repository – Configuration storage</li>
<li>Config Clients – Microservices consuming configuration</li>

<br>

---

## Application Flow

Configuration Loading Flow:

Client Microservice → Config Server → Git Repository

At startup:
- Microservice requests configuration from Config Server  
- Config Server reads configuration from Git  
- Configuration is injected into the service  

This ensures clean separation of concerns and scalability.

<br>

---

## Git Configuration Repository Structure

config-repo/
├── application.yml
├── user-service-dev.yml
├── user-service-prod.yml
├── order-service-dev.yml
└── order-service-prod.yml

Configuration naming pattern:

<br>

---

## Config Server Implementation

### Dependency

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-server</artifactId>
</dependency>

Main Application Class
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}

application.yml (Config Server)
server:
  port: 8888

spring:
  application:
    name: config-server

  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-org/config-repo
          default-label: main
          clone-on-start: true

<br>

Config Client (Microservice) Setup
Dependency
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>

bootstrap.yml (Client)
spring:
  application:
    name: user-service

  cloud:
    config:
      uri: http://localhost:8888
      profile: dev


<b>Note:</b> <code>bootstrap.yml</code> loads before <code>application.yml</code>, ensuring configuration is available at startup.

<br>

Configuration Fetch Example

Request made by client service:

GET http://localhost:8888/user-service/dev


Resolved configuration file:

user-service-dev.yml

<br>

Runtime Configuration Refresh (Optional)
Actuator Dependency
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

Enable Refresh Endpoint
management:
  endpoints:
    web:
      exposure:
        include: refresh

Trigger Refresh
POST http://localhost:8080/actuator/refresh

<br>
Key Concepts Implemented
<li>Centralized configuration management</li> <li>Externalized configuration</li> <li>Git-based config storage</li> <li>Profile-based environments</li> <li>Spring Cloud Config Server & Client</li> <li>Runtime refresh using Actuator</li> <br>
Best Practices Followed
<li>No secrets stored in Git</li> <li>Single source of configuration truth</li> <li>Environment-specific profiles</li> <li>Clean startup configuration flow</li> <li>Enterprise-ready design</li> <br>
Key Highlights
<li>Real-world microservices configuration design</li> <li>Clean and scalable architecture</li> <li>Strong Spring Cloud fundamentals</li> <li>Interview-ready project</li> <br>
Future Improvements
<li>Vault / AWS Secrets Manager integration</li> <li>Eureka-based Config Server discovery</li> <li>Kafka-based refresh mechanism</li> <li>Security hardening</li> <br>
Author

<b>Banti</b>
Java Backend Developer
Spring Boot | Microservices | Spring Cloud
