# 🤖 OraHermes Agent for Community

> **Production Deployment Guide & Architecture** | Maintained by JT Community.  
> 📦 **Repository:** https://github.com/JamberTechOfficial/OpenAgent  
> 🌐 **License:** MIT  

---

## 📌 Overview

**OraHermes Agent** is a full-featured AI agent system deployed on an Oracle Cloud Always Free Ubuntu instance. It provides an autonomous, multi-modal conversational AI experience powered by **NVIDIA NIM** (`nvidia/nemotron-3-ultra-550b-a55b`) with a **dual-service architecture**:

1. **Telegram Messaging Gateway (`hermes-gateway.service`)**: High-performance, low-latency bot communication using long-polling mode (zero open inbound ports required for chat).
2. **OraHermes Web Dashboard (`hermes-dashboard.service`)**: Rich interactive management UI (Sessions, Models, Logs, Cron, Skills, Plugins, Profiles, Config, Keys, Documentation) running 24/7 on `127.0.0.1:8000`.
3. **Secure Reverse Proxy & Authentication**: Nginx reverse proxy listening on port 443 (HTTPS) and port 80 (HTTP) with HTTP Basic Authentication, strictly guarding web dashboard access behind username and password verification.
4. **Headless & Resource-Optimized**: Completely purged of GUI/XRDP/Xorg overhead, allocating maximum CPU and RAM to the Python 3.11 virtual environment and AI runtime.

---

## 🗺️ Documentation Directory

| # | Guide | Description |
|---|---|---|
| 📖 | [Complete Guide (v3)](HERMES_COMPLETE_GUIDE.md) | Trilingual (EN / Urdu / Roman) end-to-end setup & operations manual |
| 01 | [Overview & Architecture](docs/01-overview.md) | Architectural layout, data flows, and security perimeter |
| 02 | [Oracle Cloud Setup](docs/01-oracle-cloud-setup.md) | Free VPS creation, credit card verification, and networking |
| 03 | [Free Server Alternatives](docs/02-free-server-alternatives.md) | Comparison across GCP, AWS, Azure, Render, and Railway |
| 04 | [OraHermes Agent Setup](docs/03-hermes-agent-setup.md) | Python 3.11 with `uv`, service installation, and environment |
| 05 | [Other AI Agents](docs/04-other-ai-agents.md) | Comparative evaluation with CrewAI, AutoGen, AutoGPT, and MetaGPT |
| 06 | [NVIDIA NIM API Guide](docs/05-nvidia-api-guide.md) | API keys, tested models, quotas, and regional verification solutions |
| 07 | [Telegram Bot Setup](docs/06-telegram-bot-setup.md) | BotFather configuration, token management, and user whitelisting |
| 08 | [Troubleshooting Guide](docs/07-troubleshooting.md) | Solutions for OOM freezing, service traps, and authentication |
| 09 | [System Architecture & Dashboard](docs/07-architecture.md) | Dual service topology, Nginx Basic Auth, and backup archive |

---

## 🏗️ Architecture Topology

```
                       [Telegram Users]                     [Web Browser]
                              │                                   │
                              │ (Outgoing Polling)                │ (HTTPS / Port 443)
                              ▼                                   ▼
                   ┌───────────────────────┐            ┌───────────────────┐
                   │ Telegram Bot Servers  │            │ Nginx Proxy (443) │
                   └──────────┬────────────┘            │ + HTTP Basic Auth │
                              │                         └─────────┬─────────┘
                              ▼                                   │
              ┌────────────────────────────────┐                  │ (127.0.0.1:8000)
              │   Oracle Cloud Free VPS        │                  │
              │                                │                  ▼
              │  [hermes-gateway.service]      │        [hermes-dashboard.service]
              │  (Systemd User Service)        │        (FastAPI / Vue SPA)
              │               │                │                  │
              │               ▼                │                  ▼
              │  [NVIDIA NIM API (Nemotron)]   │        [Sessions, Skills, Cron]
              └────────────────────────────────┴───────────────────────────┘
```

---

## ✅ What's Been Done (Real & Tested)

Every component of this repository was deployed and validated on an active Oracle Cloud server:

| Component | Status | Implementation Details |
|---|---|---|
| **Oracle Cloud VPS** | ✅ Active | Always Free AMD Micro instance running Ubuntu 20.04.6 LTS |
| **Swap Memory** | ✅ Active | 4 GB persistent swap file (`/swapfile`) preventing OOM during heavy tasks |
| **GUI & XRDP Teardown** | ✅ Purged | `xrdp`, `xorg`, `xfce4`, `lightdm`, and `gdm3` purged; freed RAM & disk |
| **NAT Rule Cleanup** | ✅ Purged | Deleted legacy 443->3389 NAT redirect; port 443 dedicated to HTTPS |
| **Python Environment** | ✅ Active | Python 3.11 with `uv` virtualenv at `/home/ubuntu/orahermes-agent/venv` |
| **OraHermes Gateway** | ✅ Active | Systemd user service `hermes-gateway.service` in polling mode |
| **OraHermes Web Dashboard**| ✅ Active | Systemd service `hermes-dashboard.service` listening on `127.0.0.1:8000` |
| **Nginx Reverse Proxy** | ✅ Active | Port 443 (HTTPS) & Port 80 (HTTP) reverse proxy with HTTP Basic Auth |
| **Access Control** | ✅ Active | Web Dashboard protected by HTTP Basic Auth; bot restricted by Telegram user ID |
| **LLM Inference** | ✅ Active | NVIDIA NIM API with `nvidia/nemotron-3-ultra-550b-a55b` (~2s latency) |
| **Backup Archive** | ✅ Preserved| Legacy configs and state safely stored in `/home/ubuntu/hermes_backup_20261029_075359/` |

---

## 🚀 Quick Start

### 1. Prerequisites
- Oracle Cloud Always Free VM (Ubuntu 20.04 or 22.04 LTS).
- NVIDIA Developer API Key from [build.nvidia.com](https://build.nvidia.com).
- Telegram Bot Token from [@BotFather](https://telegram.me/BotFather) and your Telegram User ID from [@userinfobot](https://telegram.me/userinfobot).

### 2. Configure Credentials
Add your secrets to `~/.hermes/.env` (permissions `0600`):
```bash
NVIDIA_API_KEY=<your-nvidia-api-key>
TELEGRAM_BOT_TOKEN=<your-telegram-bot-token>
TELEGRAM_ALLOWED_USERS=<your-telegram-user-id>
```

### 3. Service Management Commands

#### Telegram Gateway Service (User-level)
```bash
# Check status
systemctl --user status hermes-gateway

# Restart service
systemctl --user restart hermes-gateway

# View live polling logs
journalctl --user -u hermes-gateway -f
```

#### OraHermes Web Dashboard Service (System-level)
```bash
# Check status
sudo systemctl status hermes-dashboard

# Restart service
sudo systemctl restart hermes-dashboard

# View dashboard logs
journalctl -u hermes-dashboard -n 50 --no-pager
```

#### Nginx Reverse Proxy
```bash
# Test Nginx configuration syntax
sudo nginx -t

# Reload or restart Nginx
sudo systemctl reload nginx
```

---

## 🔐 Accessing the Web Dashboard

1. Navigate to `https://<your-server-ip>/` in your web browser.
2. Accept the self-signed SSL certificate prompt.
3. Enter your HTTP Basic Auth credentials (`admin` / `<your-dashboard-password>`).
4. Access the full OraHermes management interface:
   - **Sessions**: Monitor and review conversations
   - **Models**: Switch or configure inference endpoints
   - **Logs**: Real-time agent event stream
   - **Cron**: Automated task schedules
   - **Skills & Plugins**: Custom tools and integrations
   - **Config & Keys**: Runtime parameter inspection

---

## ⚠️ Security & Zero-Secrets Policy

- **No credentials or secrets in Git**: All documentation and examples in this repository use `<placeholder>` values.
- **Excluded by `.gitignore`**: `.agents/`, `.gemini/`, `*.key`, `*.pem`, `.env`, and virtual environment directories are strictly excluded from version control.
- **Fail2ban protection**: Protects SSH on port 22 against automated brute-force attacks.

---

## 🤝 Community & Support

- **Repository**: [JamberTechOfficial/OpenAgent](https://github.com/JamberTechOfficial/OpenAgent)
- **Upstream Agent**: [jasperan/orahermes-agent](https://github.com/jasperan/orahermes-agent)
- **NVIDIA NIM Portal**: [build.nvidia.com](https://build.nvidia.com)

*Crafted with precision by JT Community — Real tests, real code, real reliability.*
