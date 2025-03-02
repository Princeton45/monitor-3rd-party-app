# Redis Monitoring with Prometheus and Grafana

## Project Overview

In this project, I set up comprehensive monitoring for Redis running in a Kubernetes cluster using the Prometheus monitoring stack. The solution provides real-time metrics visualization and automated alerting when Redis experiences issues.

![diagram](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/diagram.png)

## Technologies Used

- Kubernetes
- Prometheus
- Redis
- Helm
- Grafana

## Implementation Steps

### 1. Deploy Redis Exported with Helm Chart

I deployed the Redis exporter needed for proper monitoring of metrics by Prometheus so that it can transform the Redis metrics into a format that Prometheus can understand and expose the metrics via an HTTP endpoint that Prometheus can scrape at regular intervals.

`helm repo add prometheus-community https://prometheus-community.github.io/helm-charts`
`helm repo update`

I overrided some default values from the helmchart 

`redis-values.yaml`
```yaml
serviceMonitor:
  enabled: true
  labels:
    release: monitoring

redisAddress: redis://redis-cart:6379
```

`helm install redis-exporter prometheus-community/prometheus-redis-exporter -f .\redis-values.yaml`

![redis-exporter](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/redis-exporter.png)

Now the redis exporter is showing as a target in Prometheus:

![redis-target](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/redis-target.png)

Now there are a bunch of metrics being exposed to Prometheus to scrape through with help of the Redis exporter

![redis-metrics1](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/redis-metrics1.png)


### 2. Creating Alert Rules for Redis

I created 2 different alert rules for Redis: 

1) Alert when Redis is down. 
2) Whether the Redis application has too many connections at once.

![redis-rules1](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/redis-rules1.png)

![redis-rules2](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/redis-rules2.png)

### 3. Import Redis Dashboard in Grafana

I utilized the `Redis Dashboard for Prometheus Redis Exporter` and imported it into Grafana to better visualize what is happening when we receive alerts and seeing more information for analyzing.

![dashboard](https://github.com/Princeton45/monitor-3rd-party-app/blob/main/images/dashboard.png)



