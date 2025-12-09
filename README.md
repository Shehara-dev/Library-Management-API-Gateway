# 🌐 API Gateway - Library Management System

The API Gateway acts as the single entry point for the Library Management System. It manages traffic between the Frontend (Next.js) and the Backend Services (Spring Boot), handling routing and CORS configurations.

## 🛠️ Tech Stack

* **Java 17**
* **Spring Boot 3**
* **Spring Cloud Gateway**

## 🏗️ Architecture

Instead of the Frontend talking directly to the Backend, it communicates through this Gateway.

```text
[Next.js Frontend]      [API Gateway]       [Backend Service]
   Port: 3000    ---->   Port: 8080   ---->    Port: 8083


✨ Key FeaturesCentralized Routing: Automatically forwards requests starting with /api to the backend service.CORS Management: Configured to allow requests specifically from the Frontend (http://localhost:3000), preventing cross-origin errors.Security: Hides the actual backend port and logic from the client.


⚙️ Configuration The gateway listens on port 8080 and routes traffic as follows
server:
  port: 8080
spring:
  cloud:
    gateway:
      globalcors:
        cors-configurations:
          '[/**]':
            allowedOrigins: "http://localhost:3000"
            allowedMethods: "*"
            allowedHeaders: "*"
      routes:
        - id: library-backend
          uri: http://localhost:8083
          predicates:
            - Path=/api/**

🚀 How to RunPrerequisitesJava 17+ installed.Library Backend must be running on port 8083.StepsClone the repository:Bashgit clone Library-Management-API-Gateway
Navigate to the folder:Bashcd library-gateway
Run the application:Bashmvn spring-boot:run

Run the application: Go LibraryManagementApplication and Right click -> click Run java
