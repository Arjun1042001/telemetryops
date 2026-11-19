# TelemetryOps — AWS OpenTelemetry Observability Platform

OpenTelemetry observability on AWS EC2 — Prometheus, Grafana, Jaeger

A hands-on AWS observability portfolio project demonstrating how a distributed microservices application can be deployed on Amazon EC2 and observed with the OpenTelemetry ecosystem.

> **Portfolio scope:** This repository documents my AWS deployment, Linux/Docker setup, troubleshooting, application validation, and observability learning. The demo application itself is based on the upstream OpenTelemetry Astronomy Shop project and is not claimed as original application code.

## What this project does

I deployed the OpenTelemetry Astronomy Shop demo on an Ubuntu EC2 instance using Docker Compose and validated the application through its storefront and shopping-cart workflow.

The environment included:

- AWS EC2
- Ubuntu Linux
- Docker and Docker Compose
- OpenTelemetry Collector
- Prometheus
- Grafana
- Jaeger
- Terraform CLI
- kubectl
- Git and GitHub

## Architecture / How it works

```text
User
  |
  v
OpenTelemetry Astronomy Shop
  |
  v
Distributed Microservices
  |
  v
OpenTelemetry SDKs / Instrumentation
  |
  v
OpenTelemetry Collector
  |
  +-------------------+-------------------+
  |                   |                   |
  v                   v                   v
Metrics              Traces              Telemetry
  |                   |
  v                   v
Prometheus           Jaeger
  |
  v
Grafana
```

### Observability Components

- **OpenTelemetry SDKs and Collector:** Collect and export metrics, traces, and telemetry from the Astronomy Shop microservices.
- **Prometheus:** Collect and query metrics from the OpenTelemetry Collector.
- **Grafana:** Visualize Prometheus metrics in dashboards.
- **Jaeger:** Trace and visualize distributed request flows across the microservices.
- **Docker Compose:** Run the OpenTelemetry demo stack, including the application, OpenTelemetry Collector, Prometheus, Grafana, and Jaeger.

## Tech stack

![AWS](https://img.shields.io/badge/AWS-%23232F3E.svg?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-425CC7.svg?style=for-the-badge&logo=opentelemetry&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C.svg?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)
![Jaeger](https://img.shields.io/badge/Jaeger-66CFE3.svg?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-%232496ED.svg?style=for-the-badge&logo=docker&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-%237B42BC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420.svg?style=for-the-badge&logo=ubuntu&logoColor=white)

## Repository structure

```text
.
├── README.md
└── docs/images/
    ├── opentelemetry-demo-home.jpg
    └── shopping-cart.jpg
```

This repository is documentation for the lab: it contains this README and the two screenshots in `docs/images/`. The demo application and observability stack itself were run from the upstream OpenTelemetry Astronomy Shop project with Docker Compose on the EC2 instance.

## Key work demonstrated

- Deployed the OpenTelemetry Astronomy Shop demo on an Ubuntu EC2 instance with Docker Compose, and validated it through the storefront and shopping-cart workflow.
- Diagnosed a Docker image pull failure (`no space left on device`) with `df -h`, `lsblk`, and `docker system df`, and fixed it by increasing the EC2 EBS volume to 30 GiB and inspecting the partition layout.
- Corrected the SSH login username after an initial SSH connection failure, and verified `kubectl` and the Terraform CLI after installing them.
- Confirmed the observability path in practice: metrics to Prometheus and Grafana, and traces to Jaeger, from the OpenTelemetry Collector.
- Terminated the temporary EC2 environment after testing to avoid unnecessary cloud cost and exposure.

## AWS Implementation

The lab was deployed on an Ubuntu EC2 instance.

Key implementation steps:

- Connected to EC2 with SSH key-based authentication.
- Installed Docker and Docker Compose.
- Installed and verified `kubectl`.
- Installed Terraform from the HashiCorp repository.
- Started the OpenTelemetry demo stack with Docker Compose.
- Validated the storefront and shopping-cart workflow from the EC2-hosted application.
- Diagnosed a Docker image pull failure caused by insufficient disk capacity.
- Increased the EC2 EBS volume to 30 GiB and inspected the partition layout with `lsblk`.
- Verified Linux and Docker storage status before continuing deployment.
- Terminated the temporary EC2 environment after testing to avoid unnecessary cloud cost and exposure.

## Troubleshooting Example

During deployment, Docker failed with:

```text
no space left on device
```

I diagnosed the issue using:

```bash
df -h
lsblk
docker system df
```

I identified low disk capacity as the cause and increased the EC2 EBS volume to 30 GiB.

I also corrected the SSH login username after an initial SSH connection failure.

## Application Validation

- Confirmed the OpenTelemetry Astronomy Shop storefront loaded successfully.
- Added an item to the shopping cart.
- Confirmed that the storefront and shopping-cart workflow operated correctly.

## Project Screenshots

### OpenTelemetry Astronomy Shop Storefront

![OpenTelemetry Astronomy Shop storefront](docs/images/opentelemetry-demo-home.jpg)

### Shopping Cart

![OpenTelemetry Astronomy Shop shopping cart](docs/images/shopping-cart.jpg)

## Security Practices

- Used SSH key-based authentication.
- Terminated temporary EC2 resources after testing.
- Avoided exposing production credentials.
- Kept this documentation limited to public deployment, troubleshooting, and validation details.

## Useful Validation Commands

```bash
docker compose ps
docker compose logs
curl -I http://localhost:8080
```

## Next Enhancements

- Add Terraform configuration to provision the EC2 instance and security group.
- Add Grafana and Prometheus dashboard screenshots.
- Add Jaeger trace screenshots.
- Add architecture diagrams.
- Add a cost and cleanup section.
- Add instructions for running the demo on Amazon EKS.

## Attribution

- OpenTelemetry Astronomy Shop: [open-telemetry/opentelemetry-demo](https://github.com/open-telemetry/opentelemetry-demo)
- OpenTelemetry: [opentelemetry.io](https://opentelemetry.io)
- Prometheus: [prometheus.io](https://prometheus.io)
- Grafana: [grafana.com](https://grafana.com)
- Jaeger: [jaegertracing.io](https://www.jaegertracing.io)
