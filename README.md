# Service-Registry

A dynamic service discovery server built on **Netflix Eureka**. All platform microservices register themselves with the Service-Registry on startup, enabling client-side load balancing and dynamic routing via the API Gateway.

---

## 👨‍🎓 Student & Project Metadata

| Requirement | Details |
|---|---|
| **Student Name** | Hansana Sandamini |
| **Student Number / ID** | `241722055` |
| **Slack Handle** | `@Hansana_Sandamini` |
| **GCP Project ID** | `eventhub-project-506715` |
| **Module** | ITS 2130 - Enterprise Cloud Architecture (ECA) |

---

## 💡 About

The **Service Registry** maintains a live directory of available microservice instances across GCP Managed Instance Groups (MIGs).

Instead of using hardcoded IP addresses or hostname mappings, microservices register themselves dynamically (e.g. `USER-SERVICE`, `EVENT-SERVICE`, `REGISTRATION-SERVICE`), enabling elastic scaling and failover across Compute Engine VM instances.

---

## ⚙️ Tech Stack

| Technology | Details |
|---|---|
| Java | 25 |
| Spring Boot | 4.1.0 |
| Spring Cloud | 2025.1.2 |
| Spring Cloud Netflix Eureka Server | Service registration & discovery |
| Spring Cloud Config Client | Fetches config from Config-Server (Remote Git) |
| Process Management | PM2 (`ecosystem.config.js`) |

---

## 🏗️ GCP Multi-Node Clustering

In GCP production, Eureka instances run across Compute Engine nodes (`vm-node-a.platform`, `vm-node-b.platform`, `vm-node-c.platform`) in a peer-aware high-availability cluster:

```yaml
eureka:
  client:
    service-url:
      defaultZone: http://vm-node-a.platform:9001/eureka, http://vm-node-b.platform:9001/eureka, http://vm-node-c.platform:9001/eureka
```

---

## 📊 Service Details

| Property | Value |
|---|---|
| Port | `9001` |
| Artifact ID | `Service-Registry` |
| Group ID | `lk.ijse.eca.eventhub` |
| Config Source | Remote Git Repository via `http://35.200.169.73:9000` (Config-Server) |
| Production Dashboard | `http://35.200.169.73:9001` |

---

## 🚀 Process Management (PM2) & Getting Started

On GCP Compute Engine VM instances, the Service Registry process is managed using **PM2**:
```bash
# Start Service Registry process via PM2
pm2 start ecosystem.config.js --only service-registry
```

> **Important:** Config-Server must be running before starting the Service-Registry.

**Manual / Local Development Startup:**
```bash
./mvnw spring-boot:run
```

Access the Eureka Dashboard locally at `http://localhost:9001` or in production at `http://35.200.169.73:9001`.
