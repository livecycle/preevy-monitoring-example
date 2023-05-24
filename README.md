# Monitoring Preevy environments using Prometheus and Grafana

1. Add the `node_exporter` service to your project's compose file

```yaml
services:
  node_exporter:
    image: quay.io/prometheus/node-exporter:latest
    container_name: node_exporter
    command:
      - '--path.rootfs=/host'
    pid: host
    restart: unless-stopped
    volumes:
      - '/:/host:ro,rslave'
    ports:
      - "9100"
```

2. Deploy the project using Preevy

`preevy up`

Copy the URL for the node_exporter service.

Repeat this step for all your environments.

3. Customize [prometheus/prometheus.yaml](./prometheus/prometheus.yaml) to add the node_exporter URLs from the deployed environments to the `targets` element.

4. Run `docker compose up -d` to start the Prometheus and Grafana services on your machine. You could also use Preevy to host the services as an environment.

5. Login to Grafana at http://localhost:9091 (default username/password is grafana/grafana). Under "dashboards", you should see the "Node Exporter full" dashboard.



