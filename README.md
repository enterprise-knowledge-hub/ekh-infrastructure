# EKH Infrastructure

This repository contains the Docker Compose configuration for deploying the basic infrastructure of the **EKH** project.

## Technology stack
* **Database:** PostgreSQL 17
* **Object Storage:** MinIO (S3-compatible)
* **Vector Database:** Qdrant
* **Message Broker:** Apache Kafka 4.0

---

## Quick start
### 1. Prepare the environment
Since the `.env` file is ignored by Git, you need to create one based on the example:
```bash
cp .env.example .env
```
After copying, open .env and set your credentials for the database and repository

### 2. Start services
Execute the command for start all containers:
```bash
docker compose up -d
```

### 3. Status check
Make sure all services are up and running and pass Healthcheck:
```bash
docker compose ps
```

---

## Access to services
After launsh, the services will be available at the following addresses:
 | Service | Internal Port | External Port (Host) | Comment |
| :--- | :--- | :--- | :--- |
| PostgreSQL | 5432 | 5432 | Project Database |
| MinIO API | 9000 | 9000 | S3 API |
| MinIO UI | 9001 | 9001 | MinIO Control Panel |
| Kafka | 9092 | 9092 | Message Broker |
| Qdrant | 6333 | 6333 | Vector Database |

### Auto setup MinIO
The first launch service ekh-minio-setup auto creates the following buckets:

* **documents**
* **audit**

### Important
* If you run services on host, use localhost:9092

* If you run services in Docker network, use ekh-kafka:9092

---

## Data storage (Volumes)
Service data is stored in named volumes, which allows it to remain available after container restarts:

* ekh_postgres_data — PostgreSQL data.
* ekh_minio_data — S3 objects.
* ekh_qdrant_data — Qdrant vectors.
* ekh_kafka_data — Kafka logs and messages.

---

## Stopping the project
To stop all containers:
```bash
docker compose down
```

To also delete data (Volumes)
```bash
docker compose down -v
```
