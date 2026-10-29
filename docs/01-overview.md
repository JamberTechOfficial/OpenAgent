# 01 — OraHermes Agent System Overview

---

## 1. Executive Summary

**OraHermes Agent** is an enterprise-grade, lightweight AI agent architecture adapted from NousResearch's Hermes system and customized for cloud deployments on resource-efficient Virtual Private Servers (VPS).

Operating on an Oracle Cloud Always Free AMD micro instance (1 vCPU, 1 GB RAM), OraHermes provides continuous autonomous capability through two decoupled operational interfaces:
1. **Telegram Messaging Gateway**: Provides immediate conversational AI and slash command automation directly within mobile and desktop Telegram clients.
2. **OraHermes Web Dashboard**: An administrative single-page application (SPA) exposing sessions, models, logs, cron triggers, skills, plugins, profiles, configuration, and API keys.

---

## 2. Key Architecture Pillars

### A. Dual Service Architecture
- **Messaging Gateway (`hermes-gateway.service`)**: Deployed as a systemd user unit with lingering enabled (`loginctl enable-linger ubuntu`). Connects to Telegram via HTTPS long-polling. Requires **no public inbound listening ports** for messaging, ensuring zero external exposure of chat ingress.
- **Web Dashboard (`hermes-dashboard.service`)**: Deployed as a system service executing FastAPI and serving the compiled Vue SPA bundle from `hermes_cli/web_dist` on `127.0.0.1:8000`.

### B. Secure Ingress & HTTP Basic Auth Perimeter
- **Nginx HTTPS Reverse Proxy**: Binds to public port 443 (HTTPS) and port 80 (HTTP).
- **Authentication**: Strictly enforces HTTP Basic Authentication against an encrypted `.htpasswd` store (`admin` and `ubuntu` accounts), returning `401 Unauthorized` for unauthenticated queries and `200 OK` for authorized traffic.
- **Host Header Rewriting**: Preserves external host headers while routing requests to internal loopback (`Host 127.0.0.1;`) to satisfy strict DNS-rebinding security middlewares (GHSA-ppp5-vxwm-4cf7).

### C. Headless Optimization & Resource Efficiency
- **GUI Teardown**: Uninstalled legacy desktop environments (`xrdp`, `xfce4`, `lightdm`, `xorg`), reclaiming ~400 MB of RAM and ~1 GB of disk storage.
- **4 GB Persistent Swap**: Configured at `/swapfile` to provide ample buffer memory for peak package compilation and inference token caching on 1 GB physical memory.
- **Python 3.11 with Astral `uv`**: Provides rapid virtual environment management and deterministic dependency resolution.

### D. LLM Inference via NVIDIA NIM
- **Base Endpoint**: `https://integrate.api.nvidia.com/v1`
- **Default Model**: `nvidia/nemotron-3-ultra-550b-a55b`
- **Latency**: ~2 seconds average response time
- **Capabilities**: Full function/tool calling and structured outputs.

### E. Backup & Disaster Recovery
- Prior state, SQLite databases (`state.db`, `kanban.db`), and configuration files were preserved in `/home/ubuntu/hermes_backup_20261029_075359/` before system migration.

---

## 3. Security & Zero-Secrets Mandate

All sensitive materials — including server IP addresses, SSH private keys, API tokens, bot secrets, and dashboard passwords — are strictly sanitized across all documentation in version control. Production environments read credentials from a local `.env` file with restrictive permissions (`chmod 600`).

---

*OraHermes Community Agent | System Overview*
