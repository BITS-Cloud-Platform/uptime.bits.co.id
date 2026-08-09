<div align="center">
  <h1>Uptime Kuma — Uptime Monitoring Service</h1>
  <p>
    <a href="https://uptime.bits.co.id">
      <img src="https://img.shields.io/badge/uptime.bits.co.id-Online-00C853?style=for-the-badge&logo=statuspage&logoColor=white" alt="uptime.bits.co.id Online" />
    </a>
  </p>
  <p>
    Production uptime monitoring for websites, APIs, and services
  </p>
  <br>
  <p>
    <img src="https://img.shields.io/badge/Uptime%20Kuma-5C2D91?style=flat&logo=uptime-kuma&logoColor=white" alt="Uptime Kuma" />
    <img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white" alt="Docker" />
    <img src="https://img.shields.io/badge/Docker%20Compose-2496ED?style=flat&logo=docker&logoColor=white" alt="Docker Compose" />
    <img src="https://img.shields.io/badge/SQLite-003B57?style=flat&logo=sqlite&logoColor=white" alt="SQLite" />
    <img src="https://img.shields.io/badge/license-MIT-green?style=flat" alt="MIT License" />
  </p>
</div>

---

## ✨ Overview

This repository contains Docker Compose deployment for [Uptime Kuma](https://github.com/louislam/uptime-kuma), a self-hosted uptime monitoring tool used to track availability and response time for websites, APIs, and internal services.

**Live instance:** [https://uptime.bits.co.id](https://uptime.bits.co.id)

---

## 🛠️ Features

| Feature | Description |
|---------|-------------|
| **Service Monitoring** | HTTP, ping, port, and browser checks |
| **Notification Channels** | Email, Telegram, Slack, Discord, and more |
| **Status Pages** | Public or private service status pages |
| **Persistent Storage** | SQLite data stored in Docker volume |
| **Auto Restart** | Container restarts unless explicitly stopped |
| **Health Check** | Container health probe for API endpoint |
| **Resource Limits** | CPU and memory limits configured |
| **Log Rotation** | JSON log rotation enabled |

---

## 🧰 Tech Stack

| Layer | Technology |
|-------|------------|
| **Application** | Uptime Kuma |
| **Runtime** | Docker, Docker Compose |
| **Storage** | SQLite in persistent volume |
| **Deployment** | Containerized self-hosted stack |

---

## 📁 Project Structure

```text
uptime.bits.co.id/
├── .env.example          # Environment template
├── docker-compose.yml    # Uptime Kuma service definition
├── README.md             # Project documentation
└── LICENSE               # MIT license
```

---

## 🚀 Quick Start

### Prerequisites

- Docker Engine 20.10+
- Docker Compose v2+
- Linux server or VM

### Setup

```bash
git clone https://github.com/BITS-Cloud-Platform/uptime.bits.co.id.git
cd uptime.bits.co.id
cp .env.example .env
docker compose up -d
```

Open dashboard at `http://localhost:3001` or configured port.

### First Run

1. Open dashboard in browser
2. Create administrator account
3. Add monitors for services
4. Configure notification channels
5. Publish status page if needed

---

## ⚙️ Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `UPTIME_KUMA_PORT` | `3001` | Host port mapped to container port 3001 |
| `UPTIME_KUMA_HOST` | `0.0.0.0` | Host interface bind address |

### Docker Compose Notes

- Persistent volume: `uptime-kuma-data`
- Health check: `/api/health`
- Restart policy: `unless-stopped`
- Memory limit: `256M`
- CPU limit: `0.5`
- Log rotation: `10m`, max `3` files

---

## 🛠️ Maintenance

```bash
# View logs
docker compose logs -f uptime-kuma

# Restart service
docker compose restart uptime-kuma

# Update image
docker compose pull uptime-kuma
docker compose up -d

# Backup data
docker run --rm -v uptime-kuma-data:/data -v $(pwd):/backup alpine \
  tar czf /backup/uptime-kuma-backup-$(date +%Y%m%d).tar.gz -C /data .
```

---

## 🔒 Security Notes

- `.env` stays out of version control
- Monitor credentials stay inside Docker volume
- Production access should sit behind reverse-proxy auth
- HTTPS should terminate at proxy layer

---

---

<div align="center">
  <strong>Uptime Kuma — Uptime Monitoring Service</strong>
  <br>
  Maintained by <a href="https://bits.co.id"><strong>Banten IT Solutions</strong></a>
</div>

## 📄 License

Distributed under MIT License. See [`LICENSE`](LICENSE).
