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
- **Heimdall** (`8011`): An application dashboard to navigate all self-hosted services from a single page.
- **DuckDNS**: Dynamic DNS updater to keep my home IP synced with my domain.
- **Speedtest Tracker** (`80`): Regularly tracks internet speed and pings to monitor ISP performance.
- **Cloudflared** (Host Mode): Secure tunnel to Cloudflare Zero Trust.

### 🎬 Arrs (Automation)
*The automation engine that organizes media.*
- **Prowlarr** (`9696`): Indexer manager that syncs search providers to Radarr and Sonarr.
- **Radarr** (`7878`): Automatically manages movie collections.
- **Sonarr** (`8989`): Automatically manages TV show series.
- **Overseerr** (`5055`): A request management and media discovery tool for the end-user to request me to purchase the media.
- **Bazarr** (`6767`): Automatically manages and downloads subtitles for your media library.
- **Agregarr** (`7171`): List aggregator for media.
- **FlareSolverr** (`8191`): Proxy server to bypass Cloudflare protection.

### 📺 Plex
*The "frontend" where media is consumed and tracked.*
- **Plex** (Host Mode / `32400`): Media server for streaming movies, TV shows, and personal media to any device.
- **Tautulli** (`8181`): Detailed monitoring and statistics for Plex usage.
- **Wrapperr** (`8282`): Generates a "Year in Review" (Spotify Wrapped style) for Plex users.

### 📚 Books
*A complete digital library for eBooks and Audiobooks.*
- **Calibre-Web Automated** (`8083`): A web interface for browsing and reading eBooks with auto-conversion features.
- **Shelfmark** (`8084`): (Formerly CWABD) A unified search engine for books.

### ⏬ Qbittorrent
*Gated by a VPN to ensure privacy and security.*
- **Gluetun** (`6881`): A specialized VPN client (NordVPN) that acts as a secure gateway for other containers.
- **qBittorrent** (`8484`): Routed through Gluetun. BitTorrent client routed entirely through Gluetun, used for Linux Distros.

### 🔧 Tools
*Daily utilities and productivity apps.*
- **Mealie** (`9925`): A recipe manager and meal planner with a clean web interface.
- **Mini-QR** (`5675`): A lightweight service for generating and managing custom QR codes.
- **Code-Server** (`8443`): VS Code (vscode) running in the browser to edit configurations directly on the server.
- **Metube** (`8081`): A web GUI for downloading videos from YouTube and other sites.

### 🎮 Minecraft
- **Minecraft Server** (`25565`): Dedicated Java Edition server managed via the `itzg/minecraft-server` image.

---