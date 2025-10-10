# rpi-docker-setup

My home Raspberry Pi setup with docker-compose. Plays nicely with openmediavault (OMV) web interface.

## 🚀 Services Included

### Core Services
- **DuckDNS** - Dynamic DNS with IPv6 support
- **MariaDB** - Database for Nextcloud
- **Nextcloud** - Personal cloud storage
- **SWAG** - Reverse proxy with Let's Encrypt SSL
- **Plex** - Media server
- **Watchtower** - Auto-updates containers
- **Pi-hole** - Network-wide ad blocking
- **Syncthing** - File synchronization

### 📊 Monitoring Stack
- **Grafana** - Beautiful dashboards (`http://your-pi:3000`)
- **Prometheus** - Metrics storage and querying
- **cAdvisor** - Container resource monitoring
- **Node Exporter** - System metrics (CPU, memory, disk, network)

## 🛠️ Quick Start

1. **Clone and configure**:
   ```bash
   git clone <this-repo>
   cd rpi-docker-setup
   cp env.example .env
   # Edit .env with your values
   ```

2. **Start all services**:
   ```bash
   docker-compose up -d
   ```

3. **Access your services**:
   - Grafana: `http://your-pi:3000`
   - Pi-hole: `http://your-pi:8080`
   - Nextcloud: `http://your-pi:82`
   - Syncthing: `http://your-pi:8384`
   - Plex: `http://your-pi:32400/web`

## 📁 Directory Structure

```
/srv/dev-disk-by-label-Toshiba/appdata/
├── grafana/          # Grafana dashboards and config
├── prometheus/       # Metrics storage
├── Nextcloud/        # Nextcloud data and database
├── plex/            # Plex configuration
├── pihole/          # Pi-hole configuration
├── syncthing/       # Syncthing configuration
└── letsencrypt/     # SSL certificates
```

For detailed monitoring setup, see [monitoring/README.md](monitoring/README.md).