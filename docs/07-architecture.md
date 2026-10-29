# 07 — OraHermes System Architecture & Web Dashboard Guide

---

## 1. System Topology Overview

OraHermes Agent utilizes a decoupled, service-oriented architecture designed to operate seamlessly on resource-constrained hardware (e.g. 1 vCPU, 1 GB RAM Always Free cloud instances).

```
[External Users]
      │
      ├──────────────────────────────┬──────────────────────────────┐
      ▼ (Telegram Mobile/Desktop)   ▼ (HTTPS Port 443)             ▼ (SSH Port 22)
┌──────────────┐             ┌─────────────────────┐        ┌──────────────┐
│ Telegram API │             │ Nginx Reverse Proxy │        │ Hardened SSH │
└──────┬───────┘             │  + Basic Auth       │        │  + fail2ban  │
       │                     └──────────┬──────────┘        └──────┬───────┘
       │ (Long Polling)                 │                          │
       ▼                                ▼ (127.0.0.1:8000)         ▼
┌─────────────────────────┐  ┌───────────────────────┐  ┌──────────────────┐
│ hermes-gateway.service  │  │ hermes-dashboard.svc │  │ Administration   │
│ (Systemd User Service)  │  │ (FastAPI / Vue SPA)   │  │ (Keys Only)      │
└──────────┬──────────────┘  └──────────┬────────────┘  └──────────────────┘
           │                            │
           ▼                            ▼
┌─────────────────────────┐  ┌───────────────────────┐
│ NVIDIA NIM API          │  │ SQLite State & Config │
│ (Nemotron 3 Ultra 550B) │  │ (~/.hermes/state.db)  │
└─────────────────────────┘  └───────────────────────┘
```

---

## 2. Dual Service Architecture

### A. Telegram Messaging Gateway (`hermes-gateway.service`)
- **Unit Scope:** User-level systemd (`~/.config/systemd/user/hermes-gateway.service`)
- **Linger Configuration:** `loginctl enable-linger ubuntu` ensures service execution persists across SSH sessions and server reboots.
- **Connection Model:** Outbound HTTPS long-polling to `api.telegram.org`.
- **Security Ingress:** Zero inbound open ports required for bot operation.
- **Runtime Command:**
  `/home/ubuntu/orahermes-agent/venv/bin/python -m gateway.run`

### B. OraHermes Web Dashboard (`hermes-dashboard.service`)
- **Unit Scope:** System-wide systemd (`/etc/systemd/system/hermes-dashboard.service`)
- **Internal Binding:** `127.0.0.1:8000` (loopback only)
- **Runtime Command:**
  `/home/ubuntu/orahermes-agent/venv/bin/hermes dashboard --host 127.0.0.1 --port 8000 --no-open --skip-build`
- **Modules Covered:**
  - **Sessions:** Live inspection of active conversation contexts
  - **Models:** Dynamic model selection and temperature calibration
  - **Logs:** Real-time stream of agent events and tool invocation traces
  - **Cron:** Scheduled execution tasks
  - **Skills & Plugins:** Custom tool definitions and plugin extensions
  - **Profiles & Configuration:** Environment and persona parameters

---

## 3. Reverse Proxy & Access Control

To safely expose the Web Dashboard over the internet without risking unauthenticated intrusion, Nginx acts as an SSL-terminating, credential-verifying reverse proxy.

### A. HTTP Basic Auth
- Auth realm: `"Restricted OraHermes Workspace"`
- Password file: `/etc/nginx/.htpasswd` (mode 0640, `chown root:www-data`)
- Users configured: `admin` and `ubuntu`
- Unauthenticated requests immediately receive `HTTP 401 Unauthorized`.

### B. Port Routing
- **Port 80 (HTTP):** Enforces HTTP Basic Auth and proxies to `127.0.0.1:8000`.
- **Port 443 (HTTPS):** Terminates TLS with high-grade ciphers (`TLSv1.2 TLSv1.3`), enforces HTTP Basic Auth, and proxies to `127.0.0.1:8000`.

### C. Host Header Isolation & DNS Rebinding Protection
OraHermes Agent incorporates loopback header validation (GHSA-ppp5-vxwm-4cf7). Nginx safely passes:
```nginx
proxy_set_header Host 127.0.0.1;
proxy_set_header X-Forwarded-Host $host;
```
This ensures the backend FastAPI server receives a trusted loopback host while preserving the caller's public IP and scheme.

---

## 4. Headless Server Optimization

To maximize resources on a 1 GB RAM cloud instance:
1. **Purged GUI Stack:** Completely removed `xrdp`, `xorg`, `xfce4`, `lightdm`, and `gdm3`.
2. **Reclaimed Resources:** ~400 MB RAM reclaimed; root filesystem reduced by ~1 GB.
3. **Cleaned IPTables NAT:** Removed legacy NAT redirect rules (such as 443->3389) to allow Nginx direct binding to port 443.
4. **4 GB Swap File:** Activated at `/swapfile` to ensure system resilience during heavy package installation or multi-turn reasoning.

---

## 5. Backup & Archival Structure

Prior deployment state and legacy configuration was archived to:
`/home/ubuntu/hermes_backup_20261029_075359/`

Structure:
```
hermes_backup_20261029_075359/
├── config/
│   ├── .env
│   ├── config.yaml
│   └── SOUL.md
├── data/
│   ├── state.db
│   └── kanban.db
├── service/
│   └── hermes-gateway.service
└── skills/
    └── *.py
```

---

## 6. Service Management Commands

```bash
# Manage Telegram Gateway (User Service)
systemctl --user {status|restart|stop|start} hermes-gateway
journalctl --user -u hermes-gateway -f

# Manage Web Dashboard (System Service)
sudo systemctl {status|restart|stop|start} hermes-dashboard
journalctl -u hermes-dashboard -n 50 --no-pager

# Manage Reverse Proxy
sudo systemctl {status|reload|restart} nginx
sudo nginx -t
```

---

*OraHermes Community Agent | Architecture Reference*
