# 📊 Monitoring Stack for Raspberry Pi Home Lab

This monitoring stack provides comprehensive observability for your Docker containers and Raspberry Pi system.

## 🚀 What You Get

- **Grafana**: Beautiful dashboards at `http://your-pi:3000`
- **Prometheus**: Metrics storage and querying at `http://your-pi:9090`
- **cAdvisor**: Container metrics at `http://your-pi:8088`
- **Node Exporter**: System metrics (CPU, memory, disk, network)

## 📈 Key Metrics Monitored

### System Level
- CPU usage, load average, temperature
- Memory usage and availability
- Disk space and I/O
- Network traffic and connections
- System uptime

### Container Level
- Per-container CPU and memory usage
- Container restart counts and status
- Network traffic per container
- Storage usage per container

### Service Health
- All your Docker services (Nextcloud, Plex, Pi-hole, etc.)
- Response times and availability
- Resource consumption trends

## 🛠️ Setup Instructions

1. **Add to your environment variables** (create `.env` if it doesn't exist):
   ```bash
   # Add this line to your .env file
   GRAFANA_ADMIN_PASSWORD=your_secure_password
   ```

2. **Deploy the entire stack** (monitoring is now integrated):
   ```bash
   # The monitoring services are now part of your main docker-compose.yml
   docker-compose up -d

   # Or to start only the monitoring services:
   docker-compose up -d prometheus grafana cadvisor node-exporter
   ```

3. **Access your dashboards**:
   - Grafana: `http://your-pi-ip:3000` (admin/your_password)
   - Prometheus: `http://your-pi-ip:9090`
   - cAdvisor: `http://your-pi-ip:8088`

4. **Import pre-built dashboards** in Grafana:
   - Dashboard ID `1860` - Node Exporter Full
   - Dashboard ID `893` - Docker and System Monitoring
   - Dashboard ID `14282` - cAdvisor Monitoring

## 🔧 Configuration

### Storage Locations
- Prometheus data: `/srv/dev-disk-by-label-Toshiba/appdata/prometheus`
- Grafana data: `/srv/dev-disk-by-label-Toshiba/appdata/grafana`

### Retention
- Prometheus keeps 15 days of metrics data
- Adjust in `monitoring-stack.yml` if you want more/less

### Port Usage
- Grafana: 3000
- Prometheus: 9090
- cAdvisor: 8088 (avoiding Pi-hole's 8080)
- Node Exporter: 9100

## 📊 Recommended Dashboards

Once Grafana is running, import these community dashboards:

1. **Node Exporter Full** (ID: 1860)
   - Complete system overview
   - CPU, memory, disk, network graphs

2. **Docker Container & Host Metrics** (ID: 10619)
   - Container resource usage
   - Docker daemon metrics

3. **cAdvisor** (ID: 14282)
   - Detailed container monitoring
   - Resource limits and usage

## 🚨 Optional: Add Alerting

To get notified when things go wrong, consider adding:
- **Alertmanager** for email/Slack notifications
- **Grafana alerts** for threshold-based notifications
- **Uptime monitoring** for external service checks

## 🔍 Troubleshooting

**Grafana won't start?**
- Check permissions on `/srv/dev-disk-by-label-Toshiba/appdata/grafana`
- Try: `sudo chown -R 472:472 /srv/dev-disk-by-label-Toshiba/appdata/grafana`

**No data in Prometheus?**
- Verify all exporters are running: `docker ps`
- Check Prometheus targets: `http://your-pi:9090/targets`

**cAdvisor permission issues?**
- Ensure Docker socket access
- May need to run with `--privileged` flag (already included)

## 🎯 Next Steps

1. Set up alerts for critical metrics
2. Add custom dashboards for your specific services
3. Consider adding log aggregation (ELK stack or Loki)
4. Set up external monitoring for internet connectivity