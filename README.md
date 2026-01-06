Fitness App – Microservices Architecture
This project is a full-stack fitness tracking and recommendation system built using a microservices architecture. It demonstrates real-world backend patterns including asynchronous communication with Kafka, centralized identity management with Keycloak, polyglot persistence, and Generative AI integration using the Google Gemini API.

The focus of this project is on scalable architecture, secure service interaction, and event-driven design.

Features
User Management: Secure registration and profile management using OAuth2.

Activity Logging: Users can log fitness activities (running, cycling, etc.).

Asynchronous Processing: Activity logs are processed asynchronously via Apache Kafka.

AI Recommendations: The Google Gemini API analyzes fitness data to provide tailored health insights.

Service Discovery: Dynamic service registration using Eureka.

Centralized Configuration: Global configuration management for all microservices.

API Gateway: Centralized routing and security enforcement.

Architecture Overview
The system consists of independent services communicating synchronously (REST) and asynchronously (Kafka).

Workflow:

Frontend (React) sends requests to the API Gateway.

API Gateway validates authentication tokens via Keycloak and routes requests.

User Service handles user data (stored in PostgreSQL).

Activity Service logs activities (stored in MongoDB) and publishes an event to Kafka.

AI Service consumes the event from Kafka, calls the Google Gemini API for insights, and stores the recommendation in MongoDB.

Tech Stack
Backend
Framework: Spring Boot 3.x, Spring Cloud

Language: Java 17

Database: PostgreSQL (User Service), MongoDB (Activity & AI Services)

Message Broker: Apache Kafka

Security: Keycloak (OAuth2 & OpenID Connect)

AI Integration: Google Gemini API

Frontend
Library: React

Build Tool: Vite

Styling: CSS

Infrastructure
Service Discovery: Netflix Eureka

Configuration: Spring Cloud Config Server

Gateway: Spring Cloud Gateway

Containerization: Docker (for Keycloak and Kafka)

Services Description
Config Server
Centralized configuration server that manages properties for all microservices, allowing changes without redeployment.

Eureka Server
A service registry that allows microservices to discover each other dynamically.

API Gateway
The entry point for all client requests. It handles routing and validates JWT tokens using Keycloak before forwarding requests to internal services.

User Service
Manages user accounts and profile data.

Tech: Spring Boot, PostgreSQL

Activity Service
Manages fitness activity logs. It acts as a Kafka Producer, sending event data whenever a new activity is logged.

Tech: Spring Boot, MongoDB, Apache Kafka

AI Recommendation Service
Acts as a Kafka Consumer. It listens for activity events, processes the data using the Google Gemini API to generate health tips, and stores them for the user.

Tech: Spring Boot, MongoDB, Apache Kafka, Google Gemini API

How to Run Locally
Prerequisites
Java 17+

Node.js 18+

Docker Desktop (Required for Kafka & Keycloak)

PostgreSQL

MongoDB

1. Start Infrastructure
Start Keycloak and Apache Kafka using Docker Compose.

Bash

docker-compose up -d
2. Start Backend Services
Run the following services in separate terminal windows in this order:

Bash

# 1. Config Server
cd configserver
./mvnw spring-boot:run

# 2. Eureka Server
cd eurekaserver
./mvnw spring-boot:run

# 3. User Service
cd userservice
./mvnw spring-boot:run

# 4. Activity Service
cd activityservice
./mvnw spring-boot:run

# 5. AI Service
cd aiservice
./mvnw spring-boot:run

# 6. API Gateway
cd gateway
./mvnw spring-boot:run
3. Start Frontend
Bash

cd fitness-app-frontend
npm install
npm run dev
The frontend application will be available at http://localhost:5173.

Author
Harish Kumar
