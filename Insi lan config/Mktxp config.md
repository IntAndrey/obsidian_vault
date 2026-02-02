docker-compose.yml
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    user: root
    volumes:
      - ./prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/var/lib/prometheus
    ports:
      - "9090:9090"
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/var/lib/prometheus'
      - '--storage.tsdb.retention.time=90d'
    restart: always

  mktxp:
    container_name: mktxp
    image: ghcr.io/akpw/mktxp:latest
    user: root
    volumes:
      - ./mktxp:/root/mktxp:rw
    ports:
      - "49090:49090"
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    volumes:
      - ./grafana/grafana:/etc/grafana/provisioning
      - grafana_data:/var/lib/grafana1
    environment:
      - GF_SECURITY_ADMIN_USER=insiMonitoring
      - GF_SECURITY_ADMIN_PASSWORD=warnever1
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
    restart: always

volumes:
  prometheus_data:
  grafana_data:

mktxp conf