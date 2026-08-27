#  Api-Gateway

A reactive API Gateway built with Spring Cloud Gateway (WebFlux). It serves as the single entry point for all client requests, routing traffic to the appropriate microservices discovered via the Service-Registry.

## 📌 Student & Project Information

| Field | Details |
|---|---|
| **Student Name** | Prashan Anupama |
| **Student Number** | 241711044 |
| **Slack Handle** | Lahiru Sanjeewa |
| **GCP Project ID** | prashan-gcp-project |
| **Submission Type** | Alternative Option (Capstone Project) |

## 📖 About

This project is part of the Enterprise Cloud Application (ECA) module in the Higher Diploma in Software Engineering (HDSE) program at the Institute of Software Engineering (IJSE). It is intended exclusively for students enrolled in this program.

Api-Gateway is the single, unified entry point for the entire ECA microservices platform. Built on the reactive WebFlux stack, it dynamically discovers downstream service instances via Eureka and routes each incoming request to the correct backend service — without clients ever needing to know individual service locations or ports.

## 🛠️ Tech Stack

| Technology | Details |
|---|---|
| **Java** | 25 |
| **Spring Boot** | 4.1.0 |
| **Spring Cloud** | 2025.1.2 |
| **Spring Cloud Gateway (WebFlux)** | Reactive API routing |
| **Spring Cloud Netflix Eureka Client** | Service discovery |
| **Spring Cloud Config Client** | Fetches config from Config-Server |
| **Spring Boot Actuator** | Health & management endpoints |

## 🔀 Routing Table

All requests go through `http://localhost:7000`. The gateway forwards them to the registered service instances.

| Route ID | Path Prefix | Target Service |
|---|---|---|
| **student-service** | `/api/v1/students/**` | `lb://STUDENT-SERVICE` |
| **program-service** | `/api/v1/programs/**` | `lb://PROGRAM-SERVICE` |
| **enrollment-service** | `/api/v1/enrollments/**` | `lb://ENROLLMENT-SERVICE` |

## ⚙️ Service Details

| Property | Value |
|---|---|
| **Port** | 7000 |
| **Artifact ID** | Api-Gateway |
| **Group ID** | lk.ijse.eca |
| **Config Source** | `http://localhost:9000` (Config-Server) |
| **Service Registry** | `http://localhost:9001/eureka` |

## 🌐 CORS

Cross-Origin Resource Sharing is configured globally to allow all origins, methods, and headers — suitable for development and the Next.js frontend webapp.

## 🏛️ How This Service Fits the Architecture

```text
                    ┌─────────────────────────────┐
                    │       Client (Webapp)       │
                    └───────────────┬─────────────┘
                                    │  HTTP
                                    ▼
                    ┌─────────────────────────────┐
                    │      Api-Gateway (7000)     │
                    │   • Reactive Routing        │
                    │   • Global CORS             │
                    │   • lb:// Dynamic Routing   │
                    └───────────────┬─────────────┘
                                    │  lb://
        ┌───────────────────────────┼───────────────────────────┐
        ▼                           ▼                           ▼
┌───────────────┐       ┌───────────────────┐       ┌──────────────────────┐
│STUDENT-SERVICE│       │  PROGRAM-SERVICE  │       │  ENROLLMENT-SERVICE  │
└───────────────┘       └───────────────────┘       └──────────────────────┘
        ▲
        │ registers & fetches config
┌──────────────────────────────────┐
│ Service-Registry / Config-Server │
└──────────────────────────────────┘
```

## 🚀 Getting Started

Follow the lecture guidelines, refer to the lecture video for more information and how to get started correctly.

⚠️ **Important:** Config-Server and Service-Registry must be running before starting the Api-Gateway.

### 🔢 Startup Order

| Step | Service | Port |
|---|---|---|
| 1️⃣ | Config-Server | 9000 |
| 2️⃣ | Service-Registry | 9001 |
| 3️⃣ | Api-Gateway | 7000 |
| 4️⃣ | Domain services (Student, Program, Enrollment) | Random / 0 |

### ▶️ Run the Service

```bash
./mvnw spring-boot:run
```
The gateway will be available at: `http://localhost:7000`

## 📄 License

This project was developed as part of the Enterprise Cloud Architecture university module (Capstone Project — Alternative Option).
