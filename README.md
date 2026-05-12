Self-Hosted Private Cloud
A complete self-hosted private cloud running four services in Docker containers — replacing Google Drive, LastPass, Netflix, and UptimeRobot with open-source, self-hosted alternatives.
One docker compose up -d command deploys the entire stack.
Services
ServiceReplacesPortDescriptionNextcloudGoogle Drive / Dropbox8080File sync, sharing, calendar, contactsVaultwardenBitwarden / LastPass8081Password manager (Bitwarden-compatible)JellyfinNetflix / Plex8096Media server for movies, music, photosUptime KumaUptimeRobot3001Service monitoring dashboard
Quick Start
Prerequisites

Docker Desktop installed
4GB+ free RAM

Deploy
bashgit clone https://github.com/tejansree21/self-hosted-cloud.git
cd self-hosted-cloud
mkdir nextcloud-files media
docker compose up -d
Access

Nextcloud: http://localhost:8080 (admin / changeme123)
Vaultwarden: http://localhost:8081
Jellyfin: http://localhost:8096
Uptime Kuma: http://localhost:3001

Architecture
docker-compose.yml
├── Nextcloud      (port 8080) ── volumes: nextcloud_data, ./nextcloud-files
├── Vaultwarden    (port 8081) ── volumes: vaultwarden_data
├── Jellyfin       (port 8096) ── volumes: jellyfin_config, jellyfin_cache, ./media
└── Uptime Kuma    (port 3001) ── volumes: uptime_data
All data persists in Docker volumes and bind mounts. Containers auto-restart on failure.
Management
bash# Start all services
docker compose up -d

# Stop all services
docker compose down

# View logs
docker compose logs -f

# Restart a specific service
docker restart nextcloud

# Check status
docker ps
Tech Stack

Docker + Docker Compose
Nextcloud (PHP/Apache)
Vaultwarden (Rust — lightweight Bitwarden server)
Jellyfin (.NET — open-source media system)
Uptime Kuma (Node.js — monitoring)

Next Steps

Add Caddy reverse proxy for HTTPS and custom domains
Set up Tailscale for secure remote access
Add automated backups with restic
Move to dedicated hardware (mini PC or Raspberry Pi) for 24/7 operation

Built By
Tejan Sree — LinkedIn
License
MIT