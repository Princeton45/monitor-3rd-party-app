# Redis Monitoring with Prometheus and Grafana

## Project Overview

In this project, I set up comprehensive monitoring for a Redis instance using Prometheus and Grafana in a Kubernetes environment. I configured alerts for downtime and connection overload while creating visual dashboards for real-time monitoring.

## Technologies Used

- Kubernetes
- Prometheus
- Redis
- Helm
- Grafana

## Implementation Steps

### 1. Redis Deployment on Kubernetes

I deployed a Redis service in my Kubernetes cluster using manifests that defined the deployment and service components.

*[Suggestion: Add screenshot of successful Redis deployment in Kubernetes dashboard or terminal output showing Redis pods running]*

### 2. Redis Exporter Implementation

I used Helm to deploy the Prometheus Redis Exporter, which collects and exposes Redis metrics for Prometheus to scrape.

```bash
helm install redis-exporter prometheus-community/prometheus-redis-exporter