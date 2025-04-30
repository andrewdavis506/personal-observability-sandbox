# Personal Observability Lab

A local observability sandbox using Docker Compose to run Prometheus, Grafana, Loki, Promtail, Node Exporter, and a fake log generator. Useful for exploring how logs and metrics flow through a modern monitoring stack without deploying to production.

## What's Included

- **Grafana** – data visualization
- **Loki** – log aggregation and querying
- **Promtail** – lightweight log shipping
- **Prometheus** – metrics collection and querying
- **Node Exporter** – system metrics source
- **Fake Logger (BusyBox)** – simulates log activity

## Getting Started

Clone the repo, then:

```bash
docker-compose up --build
```

Access services:

- Grafana: [http://localhost:3000](http://localhost:3000)  
  Default login: `admin / admin`
- Prometheus: [http://localhost:9090](http://localhost:9090)
- Loki: [http://localhost:3100](http://localhost:3100)

### Prometheus

Prometheus is preconfigured to scrape itself and the Node Exporter:

- `prometheus:9090`
- `node_exporter:9100`

### Grafana

Add the following data sources:
- **Prometheus**: `http://prometheus:9090`
- **Loki**: `http://loki:3100`

Explore logs using:

```logql
{job="fake-logs"}
```

And metrics using PromQL like:

```promql
node_cpu_seconds_total
```

⚠️ Notes for Windows Users
This stack is configured to run on Docker for Windows using volume mounts compatible with the Windows file system.
Logs are written to a local folder (./logs) instead of system log files, since journald and /var/log are not available on Windows hosts.

## Why This Exists

Built as a learning tool for sandboxing observability stacks.  

## License

MIT
