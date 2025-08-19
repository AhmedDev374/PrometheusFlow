1. **First:** Login to DB
![admin_login.PNG](images/admin_login.PNG)

2. **Second:** Go to DB and Create A Table (users), add a  Field to the "users" Table
![db_users.PNG](images/db_users.PNG)

3. **Forth:** Add Data to the User
![db_users_data.PNG](images/db_users_data.PNG)

4. **last:** Data will show on frontEnd & BackEnd
![back_end.PNG](images/back_end.PNG)
![fontend.PNG](images/fontend.PNG)

---

# PrometheusFlow

> A lightweight, containerized monitoring stack with Prometheus, Grafana, and Alertmanager, providing real‑time metrics, dashboards, and alerting out of the box.

---

##  Table of Contents

- [Overview](#overview)  
- [Architecture](#architecture)  
- [Prerequisites](#prerequisites)  
- [Installation & Setup](#installation--setup)  
- [Usage](#usage)  
- [Configuration & Environment Variables](#configuration--environment-variables)  
- [Project Structure](#project-structure)
- [Troubleshooting](#Troubleshooting)  
- [Contact](#contact)  
- [License](#license)

---

## Overview

PrometheusFlow is a self-contained monitoring solution for container environments. It includes:

1. **Prometheus** – For scraping and storing metrics
2. **Grafana** – For beautiful dashboards and visualization
3. **Alertmanager** – For sending notifications based on threshold-based alerts

Designed for simplicity and rapid deployment, PrometheusFlow aims to deliver full observability with minimal configuration needed.

---

## Architecture

```plaintext
┌────────────┐       ┌──────────┐       ┌───────────────┐
│            │ HTTP  │          │       │               │
│ Grafana UI ◄───────┤ Prometheus│───────► Alertmanager │
│            │       │          │       │               │
└──────┬─────┘       └────┬─────┘       └───────────────┘
       │                  │
       │ Scrapes metrics   │
       ▼                  ▼
  ┌──────────┐       ┌────────────┐
  │ Exporters│ ...   │ Your App / │
  │ (e.g.,   │       │ Container  │
  │ node-    │       │ Metrics    │
  │ exporter)│       └────────────┘
  └──────────┘
```
All services are isolated in containers and orchestrated via Docker Compose for quick and repeatable launching.

---

## Prerequisites

Ensure the following are installed on your system:

1. **Docker** – 24.x or later
2. **Docker Compose** – v2.x (included with recent Docker Desktop)

Verify:

```plaintext
docker --version
docker compose version
```

---

## Installation & Setup

1. **Clone the repository**:
```plaintext
git clone https://github.com/AhmedDev374/PrometheusFlow.git
cd PrometheusFlow
```

2. **Build and start the stack:**:
```plaintext
docker compose up --build
```
Then open .env and set your environment variables (DB credentials, ports, etc.).

3. **Access the services:**:

  - **Grafana** UI: ```http://localhost:3000```
  - **Prometheus**: ```http://localhost:9090```
  - **Alertmanager**: ```http://localhost:9093```

Default Grafana login credentials can be set via environment variables (e.g. ```GF_SECURITY_ADMIN_USER```, ```GF_SECURITY_ADMIN_PASSWORD```) — see the next section.

---

## Usage

- **Grafana** — Customize dashboards, add Prometheus as a data source, explore metrics visually.
- **Prometheus** — Query metrics, define alert rules, or examine service health.
- **Alertmanager** — Configure alert notifications via email, Slack, PagerDuty, or other channels.

Example: Create an alert in Prometheus to watch CPU usage or container memory, then route triggers through Alertmanager for immediate alerts.

---

## Configuration & Environment Variables

You can customize behavior using environment variables. Common options include:

```plaintext
GF_SECURITY_ADMIN_USER=admin
GF_SECURITY_ADMIN_PASSWORD=admin_password
PROMETHEUS_RETENTION=24h
ALERTMANAGER_RECEIVER_EMAIL=ops@example.com
```

> **Note:** Actual names may differ. Check the provided .env and docker-compose.yml in this repo to keep values consistent.

Modify the docker-compose.yml or include a .env file to override these defaults.

## Project Structure
```plaintext
PrometheusFlow/
├── docker-compose.yml        # Orchestrates the full monitoring stack
├── prometheus/
│   └── prometheus.yml         # Prometheus scrape configurations and alert rules
├── alertmanager/
│   └── alertmanager.yml       # Routing and receiver configs
├── grafana/
│   └── provisioning/          # Default dashboards and data source setup
└── README.md                  # This documentation
```
---

## Troubleshooting

| Problem                      | Solution                                                               |
| ---------------------------- | ---------------------------------------------------------------------- |
| Cannot access Grafana UI     | Ensure ports aren’t blocked and `docker compose up` ran without errors |
| Prometheus failing to scrape | Check `prometheus.yml` config and scrape targets                       |
| No alerts being sent         | Validate Alertmanager config and receiver endpoints                    |
| Stack too heavy for host     | Reduce resource limits or remove unused exporters                      |

---

## Contact

For questions or feedback, reach out to Ahmed at

1. **LinkDin**: https://eg.linkedin.com/in/ahmed-atef-elnadi-8165a51b9

---

## License

This project is licensed under the **GNU General Public License v3.0**.  
See the full license text here: [LICENSE](LICENSE).

