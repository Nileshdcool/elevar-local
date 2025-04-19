# Elevar Local - User Guide

Elevar Local is a local development environment designed to simplify working with multiple services such as MongoDB, PostgreSQL, Verdaccio, MinIO, Grafana, Prometheus, Loki, Redis, and more. It leverages Docker Compose to provide a seamless setup for these services.

---

## Table of Contents

1. [Project Structure](#project-structure)
2. [Prerequisites](#prerequisites)
3. [Getting Started](#getting-started)
4. [Services Overview](#services-overview)
    - [SMTP](#smtp)
    - [PostgreSQL](#postgresql)
    - [MongoDB](#mongodb)
    - [Verdaccio](#verdaccio)
    - [MinIO](#minio)
    - [Grafana](#grafana)
    - [Prometheus](#prometheus)
    - [Loki](#loki)
    - [Promtail](#promtail)
    - [Redis](#redis)
5. [Ignored Files and Directories](#ignored-files-and-directories)
6. [Troubleshooting](#troubleshooting)
7. [Contributing](#contributing)
8. [License](#license)

---

## Project Structure

```
elevar-local/
├── .gitignore          # Git ignore rules
├── docker-compose.yml  # Docker Compose configuration
├── README.md           # Project documentation
├── grafana_data/       # Grafana data directory
├── loki/               # Loki configuration directory
├── minio_data/         # MinIO data directory
├── mongodb_data/       # MongoDB data directory
├── mongodb_init/       # MongoDB initialization scripts
├── postgres_data/      # PostgreSQL data directory
├── prometheus/         # Prometheus configuration directory
├── redis_data/         # Redis data directory
├── verdaccio/          # Verdaccio configuration and storage
```

---

## Prerequisites

Before starting, ensure you have the following installed on your system:

- [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/)
- Basic understanding of:
  - Databases (MongoDB, PostgreSQL)
  - npm registry concepts
  - Monitoring and logging tools (Grafana, Prometheus, Loki)

---

## Getting Started

Follow these steps to set up and run the project:

1. **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd elevar-local
    ```

2. **Start the services using Docker Compose:**
    ```bash
    docker-compose up -d
    ```

3. **Access the services:**
    - **SMTP**: Access the SMTP web interface at `http://localhost:5001`.
    - **MongoDB**: Connect to `localhost:27018`.
    - **PostgreSQL**: Connect to `localhost:5433`.
    - **Verdaccio**: Access the local npm registry at `http://localhost:4873`.
    - **MinIO**: Access the MinIO console at `http://localhost:9001`.
    - **Grafana**: Access the Grafana dashboard at `http://localhost:3000`.
    - **Prometheus**: Access the Prometheus dashboard at `http://localhost:9090`.
    - **Loki**: Loki runs on `http://localhost:3100`.
    - **Redis Commander**: Access the Redis Commander UI at `http://localhost:8081`.

---

## Services Overview

### SMTP

- **Image**: `rnwood/smtp4dev:latest`
- **Ports**:
  - `5001:80` (Web interface)
  - `2526:25` (SMTP server)
- Use this service to test email functionality in your applications.

### PostgreSQL

- **Image**: `postgres`
- **Ports**: `5433:5432`
- **Data Directory**: `./postgres_data`
- **Environment Variables**:
  - `POSTGRES_USER`: `postgres`
  - `POSTGRES_PASSWORD`: `postgres`
  - `POSTGRES_DB`: `elevar`

### MongoDB

- **Image**: `mongo`
- **Ports**: `27018:27017`
- **Data Directory**: `./mongodb_data`
- **Initialization Scripts**: `./mongodb_init`
- **Environment Variables**:
  - `MONGO_INITDB_ROOT_USERNAME`: `root`
  - `MONGO_INITDB_ROOT_PASSWORD`: `password`

### Verdaccio

- **Image**: `verdaccio/verdaccio:latest`
- **Ports**: `4873:4873`
- **Storage Directory**: `./verdaccio/storage`
- **Configuration File**: `./verdaccio/conf/config.yaml`
- **Environment Variables**:
  - `VERDACCIO_AUTH_JWT_SECRET`: `your_jwt_secret`

#### Publishing a Package to Verdaccio

1. Configure your npm client:
    ```bash
    npm set registry http://localhost:4873
    ```

2. Authenticate with Verdaccio (if authentication is enabled):
    ```bash
    npm adduser --registry http://localhost:4873
    ```

### MinIO

- **Image**: `minio/minio:latest`
- **Ports**:
  - `9000:9000` (API)
  - `9001:9001` (Console)
- **Data Directory**: `./minio_data`
- **Environment Variables**:
  - `MINIO_ROOT_USER`: `minioadmin`
  - `MINIO_ROOT_PASSWORD`: `minioadmin`

### Grafana

- **Image**: `grafana/grafana:latest`
- **Ports**: `3000:3000`
- **Data Directory**: `./grafana_data`
- **Environment Variables**:
  - `GF_SECURITY_ADMIN_USER`: `admin`
  - `GF_SECURITY_ADMIN_PASSWORD`: `admin`

### Prometheus

- **Image**: `prom/prometheus:latest`
- **Ports**: `9090:9090`
- **Configuration File**: `./prometheus/prometheus.yml`

### Loki

- **Image**: `grafana/loki:latest`
- **Ports**: `3100:3100`
- **Configuration File**: `./loki/config.yml`

### Promtail

- **Image**: `grafana/promtail:latest`
- **Configuration File**: `./loki/promtail-config.yml`
- **Command**: `-config.file=/etc/promtail/config.yml`

### Redis

- **Image**: `redis:latest`
- **Ports**: `6379:6379`
- **Data Directory**: `./redis_data`
- **Command**: `["redis-server", "--save", "60", "1", "--loglevel", "warning"]`

### Redis Commander

- **Image**: `rediscommander/redis-commander:latest`
- **Ports**: `8081:8081`
- **Environment Variables**:
  - `REDIS_HOSTS`: `local:redis:6379`

---

## Ignored Files and Directories

The following directories are ignored in version control as specified in the `.gitignore` file:

- `grafana_data/`
- `loki/`
- `minio_data/`
- `mongodb_data/`
- `mongodb_init/`
- `postgres_data/`
- `prometheus/`
- `redis_data/`
- `verdaccio/`

This ensures that sensitive or large data files are not accidentally committed to the repository.

---

## Troubleshooting

- Ensure Docker is running and has sufficient resources allocated.
- Use `docker-compose logs` to view logs for individual services.
- For Verdaccio-specific issues, refer to the [Verdaccio documentation](https://verdaccio.org/docs).
- For MinIO-specific issues, refer to the [MinIO documentation](https://min.io/docs).
- For Grafana-specific issues, refer to the [Grafana documentation](https://grafana.com/docs/).

---

## Contributing

Contributions are welcome! Please fork the repository, create a feature branch, and submit a pull request.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

---