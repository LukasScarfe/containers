# 🐋 Lukas's Homelab

This repository contains the Docker Compose configurations for my homelab. The project is organized into modular stacks to ensure high availability, security, and ease of maintenance.

---

## 🏗️ Architecture Overview

The lab is divided into logical stacks. Each directory contains its own `docker-compose.yml` and a `.env` file for sensitive variables.

- **Infrastructure**: Core management and monitoring tools.
- **Arrs**: Media automation and request management.
- **Plex**: Content delivery and viewing statistics.
- **Books**: Digital library management and automation.
- **Qbittorrent**: Secure VPN-gated download clients.
- **Tools**: Productivity and utility applications.
- **Minecraft**: Dedicated gaming server.

---

## Stacks & Containers

### 🛡️ Infrastructure
*The foundation of the lab, managing connectivity and health.*
- **Portainer** (`9443`): Web-based GUI for managing Docker containers, images, and volumes.
- **Uptime Kuma** (`3001`): Self-hosted monitoring tool for tracking service uptime and heartbeats.
- **AdGuard Home** (`Host Mode`): Network-wide DNS server for ad-blocking and privacy.
- **Homepage** (`3132`): A modern, highly customizable application dashboard.
- **Heimdall** (`8011`): A simple application dashboard for navigating self-hosted services.
- **DuckDNS**: Dynamic DNS updater to keep home IP synced with a custom domain.
- **Speedtest Tracker** (`8013`): Regularly tracks internet speed and pings to monitor ISP performance.
- **Cloudflared** (`Host Mode`): Secure tunnel to Cloudflare Zero Trust for remote access.

### 🎬 Arrs (Automation)
*The automation engine that organizes media.*
- **Prowlarr** (`9696`): Indexer manager that syncs search providers to Radarr and Sonarr.
- **Radarr** (`7878`): Automatically manages movie collections.
- **Sonarr** (`8989`): Automatically manages TV show series.
- **Overseerr** (`5055`): A request management and media discovery tool.
- **Bazarr** (`6767`): Automatically manages and downloads subtitles.
- **Agregarr** (`7171`): List aggregator for media.
- **FlareSolverr** (`8191`): Proxy server to bypass Cloudflare protection.

### 📺 Plex
*The "frontend" where media is consumed and tracked.*
- **Plex** (Host Mode / `32400`): Media server for streaming movies, TV shows, and personal media.
- **Tautulli** (`8181`): Detailed monitoring and statistics for Plex usage.
- **Wrapperr** (`8282`): Generates a "Year in Review" for Plex users.

### 📚 Books
*A complete digital library for eBooks and Audiobooks.*
- **Calibre-Web Automated** (`8083`): Web interface for browsing and reading eBooks.
- **Shelfmark** (`8084`): A unified search engine for books.

### ⏬ Qbittorrent
*Gated by a VPN to ensure privacy and security.*
- **Gluetun** (`6881`): Specialized VPN client (NordVPN) acting as a secure gateway.
- **qBittorrent** (`8484`): BitTorrent client routed entirely through Gluetun.

### 🔧 Tools
*Daily utilities and productivity apps.*
- **Mealie** (`9925`): A recipe manager and meal planner.
- **Mini-QR** (`5675`): A lightweight service for generating custom QR codes.
- **Code-Server** (`8443`): VS Code running in the browser for remote.configuration.
- **Metube** (`8081`): A web GUI for downloading videos from YouTube and other sites.
- **Huginn** (`3335`): Automated Agents, not in use at all.
- **YouRLs** (`8189`): Custom URL shortener and custom tracking for each link.
- **Octoprint** (`8888`): 3D printer interface server for remote printing and tracking prints.
- **BentoPDF** (`3987`): PDF manipulation and editing tool.


### 🎮 Minecraft
- **Minecraft Server** (`25565`): Dedicated Java Edition server.

---

## 🛡️ AdGuard Home Setup

AdGuard Home is configured using **Host Networking** to ensure it can see individual device IPs for accurate logging and naming.

### ⚠️ Prerequisites (Ubuntu Host Only)
To allow AdGuard to handle DNS on port 53, Ubuntu's internal resolver stub must be disabled:

1. **Disable the DNS Stub Listener:**
   ```bash
   sudo mkdir -p /etc/systemd/resolved.conf.d
   echo -e "[Resolve]\nDNS=127.0.0.1\nDNSStubListener=no" | sudo tee /etc/systemd/resolved.conf.d/adguardhome.conf