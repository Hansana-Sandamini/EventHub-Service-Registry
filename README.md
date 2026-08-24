# Service-Registry

A service discovery server built on Netflix Eureka. All microservices register themselves here on startup, allowing the API Gateway and other services to locate them dynamically by name rather than hardcoded URLs.

## About

The Service Registry uses **Netflix Eureka / Spring Cloud Eureka** to maintain a registry of available EventHub microservices.

Instead of using fixed service locations, microservices register themselves with Eureka and discover other services through the registry.

## Tech Stack

| Technology | Details |
|---|---|
| Java | 25 |
| Spring Boot | 4.1.0 |
| Spring Cloud | 2025.1.2 |
| Spring Cloud Netflix Eureka Server | Service discovery |
| Spring Cloud Config Client | Fetches config from Config-Server |

## How It Works

The Service-Registry acts as the central directory for the microservices architecture. When a service starts, it registers with this server. The API Gateway queries this registry to resolve service locations using load-balanced URIs (e.g., `lb://USER-SERVICE`).

## Service Details

| Property | Value                                   |
|---|-----------------------------------------|
| Port | `9001`                                  |
| Artifact ID | `Service-Registry`                      |
| Group ID | `lk.ijse.eca.eventhub`                  |
| Config Source | `http://localhost:9000` (Config-Server) |

## Getting Started

> **Important:** Config-Server must be running before starting the Service-Registry, as it fetches its configuration from Config-Server on startup.

**Startup order:**
1. Config-Server (`9000`)
2. **Service-Registry** (`9001`)
3. Other services...

```bash
./mvnw spring-boot:run
```

The Eureka dashboard will be available at: `http://localhost:9001`


