# Uptime Kuma — Uptime Monitoring Service

[![Status](https://img.shields.io/badge/status-live-brightgreen)](https://uptime.bits.co.id)
[![Uptime Kuma](https://img.shields.io/badge/powered%20by-Uptime%20Kuma-blue)](https://github.com/louislam/uptime-kuma)

> Production-grade uptime monitoring solution deployed and managed by **Banten IT Solutions**  
> 🌐 [https://bits.co.id](https://bits.co.id)

---

## 📋 Overview

This repository contains the **Docker Compose deployment** for [Uptime Kuma](https://github.com/louislam/uptime-kuma), a self-hosted, open-source uptime monitoring tool. It tracks the availability and response time of websites, APIs, and services — with rich notifications, beautiful status pages, and a modern dashboard.

**Live instance:** [https://uptime.bits.co.id](https://uptime.bits.co.id)

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────┐
│                   Docker Host                      │
│  ┌────────────────────────────────────────────┐   │
│  │           Uptime Kuma Container              │   │
│  │  ┌──────────┐   ┌───────────────────────┐   │   │
│  │  │  Node.js  │──▶│  SQLite (persistent)  │   │   │
│  │  └──────────┘   └───────────────────────┘   │   │
│  │         │                                      │   │
│  │         ▼                                      │   │
│  │  ┌───────────────────────────────────────┐   │   │
│  │  │  Health Check Engine (HTTP/Ping/Port)  │   │   │
│  │  └───────────────────────────────────────┘   │   │
│  └────────────────────────────────────────────┘   │
│         │                                          │
│         ▼                                          │
│  ┌────────────────────────────────────────────┐   │
│  │  Persistent Volume: uptime-kuma-data        │   │
│  └────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

- Docker Engine ≥ 20.10.x
- Docker Compose ≥ 2.x
- A Linux server with public access (for external monitoring)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-org/uptime-kuma.git
cd uptime-kuma

# 2. Create environment configuration
cp .env.example .env
# Edit .env to customize port and host if needed

# 3. Launch the service
docker compose up -d
```

The dashboard will be available at **http://localhost:3001** (or your configured port).

### First-Time Setup

1. Open the dashboard in your browser
2. Create an administrator account
3. Start adding monitors for your services
4. Configure notification channels (Email, Telegram, Slack, Discord, etc.)
5. (Optional) Publish a public status page

---

## ⚙️ Configuration

### Environment Variables

| Variable            | Default       | Description                            |
|---------------------|---------------|----------------------------------------|
| `UPTIME_KUMA_PORT`  | `3001`        | Host port mapped to container port 3001|
| `UPTIME_KUMA_HOST`  | `0.0.0.0`     | Host interface to bind to              |

### Docker Compose

The service includes:

- **Auto-restart** — container restarts unless explicitly stopped
- **Health check** — validates the API health endpoint every 30 seconds
- **Resource limits** — capped at 0.5 CPU cores and 256 MB RAM
- **Log rotation** — capped at 10 MB per file, maximum 3 rotated files
- **Named volume** — `uptime-kuma-data` persists the SQLite database and monitor configurations

---

## 🛠️ Maintenance

```bash
# View logs
docker compose logs -f uptime-kuma

# Restart service
docker compose restart uptime-kuma

# Update to latest version
docker compose pull uptime-kuma
docker compose up -d

# Backup monitor data
docker run --rm -v uptime-kuma-data:/data -v $(pwd):/backup alpine \
  tar czf /backup/uptime-kuma-backup-$(date +%Y%m%d).tar.gz -C /data .
```

---

## 🔒 Security Considerations

- The `.env` file contains environment-specific configuration and is **excluded** from version control via `.gitignore`
- Sensitive monitor credentials (passwords, API tokens, notification keys) are stored **only** in the Docker volume, never in this repository
- Access to the live instance should be restricted with reverse-proxy authentication (e.g., Authelia, OAuth2 Proxy) for production deployments
- All traffic is served over **HTTPS** via a TLS-terminating reverse proxy (e.g., Nginx, Caddy, Traefik)

---

## 🤝 Credits & Maintainer

<p align="center">
  <a href="https://bits.co.id">
    <img src="https://bits.co.id/assets/images/logo.png" alt="Banten IT Solutions" width="200"/>
  </a>
</p>

This project is **deployed, maintained, and monitored** by

### **Banten IT Solutions**

| | |
|---|---|
| **Website** | [https://bits.co.id](https://bits.co.id) |
| **Services** | Web Development, IT Infrastructure, Cloud Solutions, Monitoring |
| **Location** | Banten, Indonesia |

For professional IT solutions — including server monitoring, cloud infrastructure, and web development — contact **Banten IT Solutions**.

---

## 📄 License

This deployment configuration is provided under the [MIT License](LICENSE).  
The underlying [Uptime Kuma](https://github.com/louislam/uptime-kuma) software is licensed under the MIT License by Louis Lam.
