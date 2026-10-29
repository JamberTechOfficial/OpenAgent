# Project: Hermes to OraHermes Migration & Community Agent Deployment

## Architecture
- **Server Infrastructure**: Oracle Cloud Ubuntu 20.04.6 LTS (`ubuntu@<your-server-ip>`).
- **Target Agent**: `orahermes-agent` (`https://github.com/jasperan/orahermes-agent`), Python 3.11+ via `uv` venv.
- **Service Management**: Dual services via Systemd:
  1. `hermes-gateway.service`: Systemd user service (`systemctl --user`) running Telegram messaging gateway in long-polling mode.
  2. `hermes-dashboard.service`: System-wide systemd service running OraHermes Web Dashboard on `127.0.0.1:8000`.
- **Security & Ingress**: Nginx HTTPS reverse proxy on port 443 with HTTP Basic Auth (`admin` / `<dashboard-password>`) proxying to the local Web Dashboard, with XRDP/Xorg/GUI completely purged.
- **LLM Provider**: NVIDIA NIM API (`https://integrate.api.nvidia.com/v1`) using `nvidia/nemotron-3-ultra-550b-a55b`.
- **Messaging Interface**: Telegram Bot `@jtcommunitybot` (token `<telegram-bot-token>`, allowed user `<telegram-user-id>`).
- **Storage**: Lightweight file-backed session state with Oracle DB optional adapter.
- **Local Workspace**: Documentation repository `d:\RDX\HARMES FOR JT COMMUNITY` synchronized with GitHub `https://github.com/JamberTechOfficial/OpenAgent` with strict secret isolation (`.gitignore`).

---

## Feature Inventory
| # | Feature | Description | Milestone | Source |
|---|---------|-------------|-----------|--------|
| 1 | Hermes Service Decommission | Stop and disable `hermes-gateway.service` (user systemd) and terminate lingering installer screen session | M1 | ORIGINAL_REQUEST §R1, server survey |
| 2 | Hermes Data & Config Backup | Archive existing config (`.env`, `config.yaml`, `SOUL.md`), SQLite databases (`state.db`, `kanban.db`), skills, and unit file into `/home/ubuntu/hermes_backup_*/` | M1 | ORIGINAL_REQUEST §R1, server survey |
| 3 | orahermes-agent Repo Clone & Setup | Clone `https://github.com/jasperan/orahermes-agent` and provision Python 3.11 venv with `uv` and dependencies | M1 | ORIGINAL_REQUEST §R2, repo spec |
| 4 | Agent Environment & Credentials Config | Configure `~/.hermes/.env` and `config.yaml` with NVIDIA NIM API key, base URL, model, Telegram bot token, and allowed user ID | M1 | ORIGINAL_REQUEST §R2, repo spec |
| 5 | orahermes-agent Systemd Service | Install and configure systemd service, enable with linger, and start in active running state | M1 | ORIGINAL_REQUEST §R2, repo spec |
| 6 | Service Startup & Journalctl Clean Execution | Verify journalctl logs show successful initialization, Telegram polling connection, and zero fatal crashes | M1 | Acceptance Criteria |
| 7 | Telegram & NVIDIA Live Integration Verification | Verify agent authenticates with Telegram Bot API and NVIDIA NIM API, responding to authorized user | M2 | Acceptance Criteria |
| 8 | Git Hygiene & Secret Leak Prevention | Create comprehensive `.gitignore` preventing `.agents/`, `*.key`, `*.pem`, `.env`, and credential leakage | M3 | Local survey, Acceptance Criteria |
| 9 | Sensitive Data Sanitization | Sanitize `HERMES_COMPLETE_GUIDE.md` replacing live server IP `<your-server-ip>` and key paths with safe placeholders | M3 | Local survey |
| 10 | Documentation Update & Rebranding | Update `README.md`, `HERMES_COMPLETE_GUIDE.md`, and `docs/` to document `orahermes-agent` architecture, setup, and systemd management | M3 | ORIGINAL_REQUEST §R3 |
| 11 | GitHub Repository Synchronization | Initialize local git (`main` branch), pull remote history/license, commit sanitized documentation, and push to GitHub `OpenAgent` | M3 | ORIGINAL_REQUEST §R3 |
| 12 | Forensic Integrity & Security Audit | Independent auditor verification confirming authentic service deployment, clean logs, zero secret leakage in git history | M4 | Acceptance Criteria |
| 13 | Complete GUI & RDP Package Teardown | Stop, disable, and purge `xrdp`, `xfce4`, `xorg`, `lightdm`/`gdm3`, and GUI packages to free RAM, CPU, and disk | M2B | Follow-up 2026-10-29T08:38:03Z |
| 14 | Remove iptables 443->3389 NAT Redirect | Delete legacy iptables NAT PREROUTING redirect rule forwarding port 443 to 3389 and persist clean iptables | M2B | Follow-up 2026-10-29T08:38:03Z |
| 15 | Deploy OraHermes Web Dashboard Service | Deploy OraHermes Web Dashboard (`hermes dashboard` web UI covering Sessions, Models, Logs, Cron, Skills, Plugins, Profiles, Config, Keys, Documentation) as a persistent 24/7 systemd service | M2B | Follow-up 2026-10-29T08:38:03Z |
| 16 | Web Dashboard Authentication & Reverse Proxy | Configure Reverse Proxy (Nginx) listening on port 443/80 with HTTP Basic Auth (`admin` / `<dashboard-password>`) proxying to the local dashboard port, strictly enforcing login credentials | M2B | Follow-up 2026-10-29T08:38:03Z |
| 17 | Dashboard & Auth Documentation | Document OraHermes Web Dashboard access, systemd service management, and reverse proxy login protection in README & docs using credential placeholders | M3 | Follow-up 2026-10-29T08:38:03Z |

---

## Milestones
| # | Name | Scope | Dependencies | Status |
|---|------|-------|-------------|--------|
| M1 | Server Service Migration & orahermes-agent Deployment | Stop/disable old service, clean installer screen, backup configs/data to designated archive, clone orahermes-agent, setup Python 3.11 venv, configure .env/config.yaml, enable & start systemd service, verify journalctl | none | DONE |
| M2 | Telegram Bot & NVIDIA API Live Integration Verification | Verify live long-polling, Telegram handshake, NVIDIA NIM API interaction, and slash command response | M1 | DONE |
| M2B | GUI Teardown, OraHermes Web Dashboard & Secure Reverse Proxy | Purge xrdp/xfce4/xorg, remove iptables 443->3389 NAT rule, deploy OraHermes Web Dashboard systemd service, configure Nginx reverse proxy on port 443 with HTTP Basic Auth (admin / `<dashboard-password>`) | M1 | DONE |
| M3 | Documentation Rebranding, Git Hygiene & GitHub Sync | Create .gitignore, sanitize guides, rebrand README & docs including dashboard & auth guides, init git main branch, commit and push to OpenAgent | M1, M2B | IN_PROGRESS |
| M4 | Final Acceptance Verification & Forensic Integrity Audit | Systematic checks (systemd status, journal logs, live Telegram response, Web Dashboard 401/200 auth verification, Git commit cleanliness) and binary veto audit | M2, M2B, M3 | PLANNED |

---

## Interface Contracts
### Server Service ↔ Systemd
- Unit Name: `hermes-gateway.service` managed via user systemd (`systemctl --user`).
- Dashboard Unit Name: `hermes-dashboard.service` managed via system-wide systemd (`systemctl`).
- Linger: `loginctl show-user ubuntu --property=Linger` -> `Linger=yes`.
- ExecStart Gateway: `/home/ubuntu/orahermes-agent/venv/bin/python -m gateway.run` (or `hermes gateway run --replace`).
- ExecStart Dashboard: `/home/ubuntu/orahermes-agent/venv/bin/hermes dashboard --host 127.0.0.1 --port 8000 --no-open --skip-build`.
- Working Directory: `/home/ubuntu/orahermes-agent`.
- Environment File: `/home/ubuntu/.hermes/.env` (mode 0600).

### Agent ↔ NVIDIA NIM API
- Base URL: `https://integrate.api.nvidia.com/v1`
- Model: `nvidia/nemotron-3-ultra-550b-a55b`
- Header / Auth: `Authorization: Bearer <NVIDIA_API_KEY>`

### Agent ↔ Telegram Bot API
- Auth: `Bot <telegram-bot-token>`
- Mode: Long-polling (`[Telegram] Connected to Telegram (polling mode)`)
- Access Control: `TELEGRAM_ALLOWED_USERS=<telegram-user-id>`

### Reverse Proxy ↔ Web Dashboard
- Ingress Ports: TCP 443 (HTTPS), TCP 80 (HTTP).
- Authentication: HTTP Basic Auth (`admin` / `<dashboard-password>`).
- Upstream: `http://127.0.0.1:8000`.

### Local Workspace ↔ GitHub Remote
- Remote URL: `https://github.com/JamberTechOfficial/OpenAgent.git`
- Branch: `main`
- Secret Isolation: `.gitignore` must ignore `.agents/`, `*.key`, `*.pem`, `.env`, `node_modules/`, `venv/`.

---

## Code Layout
- Server Agent Location: `/home/ubuntu/orahermes-agent/`
- Server Virtual Environment: `/home/ubuntu/orahermes-agent/venv/`
- Server Agent Config: `/home/ubuntu/.hermes/.env`, `/home/ubuntu/.hermes/config.yaml`
- Server Backup Location: `/home/ubuntu/hermes_backup_YYYYMMDD_HHMMSS/`
- Local Project Docs: `d:\RDX\HARMES FOR JT COMMUNITY\README.md`, `HERMES_COMPLETE_GUIDE.md`, `docs/*.md`
- Local Git Config: `d:\RDX\HARMES FOR JT COMMUNITY\.gitignore`, `.git/`
