# 03 — OraHermes Agent Setup & Deployment Guide

> **Status:** ✅ Tested & Production Deployed on Oracle Cloud Ubuntu 20.04 | AMD Micro | 1 GB RAM  
> **Target Agent:** `orahermes-agent` (`https://github.com/jasperan/orahermes-agent`) with Python 3.11 via `uv`  

---

## Table of Contents

1. [What is OraHermes Agent?](#1-what-is-orahermes-agent)
2. [Prerequisites](#2-prerequisites)
3. [⚠️ CRITICAL: Add Swap BEFORE Installing](#3-️-critical-add-swap-before-installing-tested-)
4. [Headless Server Optimization: GUI & XRDP Purge](#4-headless-server-optimization-gui--xrdp-purge)
5. [Install System Packages & Python 3.11 with uv](#5-install-system-packages--python-311-with-uv)
6. [Clone and Setup orahermes-agent](#6-clone-and-setup-orahermes-agent)
7. [Configure Credentials and NVIDIA NIM Model](#7-configure-credentials-and-nvidia-nim-model)
8. [Deploy Telegram Gateway Systemd Service](#8-deploy-telegram-gateway-systemd-service)
9. [Deploy OraHermes Web Dashboard Systemd Service](#9-deploy-orahermes-web-dashboard-systemd-service)
10. [Configure Nginx HTTPS Reverse Proxy with HTTP Basic Auth](#10-configure-nginx-https-reverse-proxy-with-http-basic-auth)
11. [Verification & Testing](#11-verification--testing)
12. [Useful Management Commands](#12-useful-management-commands)
13. [Common Errors & Fixes](#13-common-errors--fixes)

---

## 1. What is OraHermes Agent?

**OraHermes Agent** is an enhanced, open-source AI agent platform built upon NousResearch's Hermes architecture, optimized by Jasperan and the community for cloud deployments, lightweight state persistence, and multi-interface operations.

It features:
- **Telegram Bot Messaging Gateway**: Operates in resilient long-polling mode (outbound connection only).
- **Interactive Web Dashboard**: Full management UI covering Sessions, Models, Logs, Cron schedules, Skills, Plugins, Profiles, Configuration, and Keys.
- **NVIDIA NIM API Integration**: Powered by `nvidia/nemotron-3-ultra-550b-a55b` for tool-use and rapid conversational response without needing a local GPU.
- **Minimal Footprint**: Runs inside an isolated Python 3.11 virtual environment powered by `uv`.

---

## 2. Prerequisites

| Requirement | Description | Setup Guide |
|---|---|---|
| Ubuntu 20.04/22.04 LTS Server | Free Oracle Cloud VPS | `01-oracle-cloud-setup.md` |
| NVIDIA NIM API Key | Free 1,000 credits developer key | `05-nvidia-api-guide.md` |
| Telegram Bot Token | Bot token from [@BotFather](https://telegram.me/BotFather) | `06-telegram-bot-setup.md` |
| Telegram User ID | Numeric ID from [@userinfobot](https://telegram.me/userinfobot) | `06-telegram-bot-setup.md` |
| Nginx & Apache2-utils | Reverse proxy and HTTP basic auth utilities | Documented below |

---

## 3. ⚠️ CRITICAL: Add Swap BEFORE Installing (TESTED ✅)

On 1 GB RAM micro instances, swap is strictly required. Without swap, Python dependency compilation or memory caching will trigger an out-of-memory kernel lockup.

```bash
# 1. Check existing swap
free -h

# 2. Allocate 4 GB swap file
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# 3. Persist across server reboots
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# 4. Verify swap is active
free -h
# Swap: 4.0Gi should now be visible
```

---

## 4. Headless Server Optimization: GUI & XRDP Purge

Purging graphical desktop environments (XFCE4, Xorg, LightDM, XRDP) frees ~400 MB of system RAM and ~1 GB of disk space.

```bash
# Stop and disable desktop services
sudo systemctl stop xrdp xrdp-sesman lightdm gdm3 || true
sudo systemctl disable xrdp xrdp-sesman lightdm gdm3 || true

# Purge packages
sudo DEBIAN_FRONTEND=noninteractive apt-get purge -y xrdp xorg 'xfce4*' 'lightdm*' 'gdm3*' 'xserver*' xorg-docs-core
sudo DEBIAN_FRONTEND=noninteractive apt-get autoremove -y --purge
sudo apt-get clean

# Remove legacy NAT port redirection (443 -> 3389)
sudo iptables -t nat -D PREROUTING 1 2>/dev/null || true
sudo netfilter-persistent save
```

---

## 5. Install System Packages & Python 3.11 with uv

```bash
# Base tools
sudo apt-get update -y
sudo apt-get install -y git curl fail2ban libatomic1 software-properties-common nginx apache2-utils

# Python 3.11 PPA
sudo add-apt-repository -y ppa:deadsnakes/ppa
sudo apt-get update -y
sudo apt-get install -y python3.11 python3.11-venv python3.11-dev

# Astral uv
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.cargo/env
```

---

## 6. Clone and Setup orahermes-agent

```bash
cd ~
git clone https://github.com/jasperan/orahermes-agent.git
cd ~/orahermes-agent

# Create Python 3.11 virtual environment
uv venv venv --python python3.11
source venv/bin/activate

# Install package in editable mode with dependencies
uv pip install -e .

# Confirm binary runs
~/orahermes-agent/venv/bin/hermes --version
```

---

## 7. Configure Credentials and NVIDIA NIM Model

Create `~/.hermes/.env` with strict permissions:
```bash
mkdir -p ~/.hermes
cat > ~/.hermes/.env << 'EOF'
NVIDIA_API_KEY=<your-nvidia-api-key>
TELEGRAM_BOT_TOKEN=<your-telegram-bot-token>
TELEGRAM_ALLOWED_USERS=<your-telegram-user-id>
EOF
chmod 600 ~/.hermes/.env
```

Set model parameters:
```bash
~/orahermes-agent/venv/bin/hermes config set model.provider nvidia
~/orahermes-agent/venv/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1
~/orahermes-agent/venv/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

---

## 8. Deploy Telegram Gateway Systemd Service

Run the messaging gateway as a background user systemd service:

```bash
# Enable linger so user services persist after logout
sudo loginctl enable-linger ubuntu

# Setup systemd user directory
mkdir -p ~/.config/systemd/user
cat > ~/.config/systemd/user/hermes-gateway.service << 'EOF'
[Unit]
Description=Hermes Telegram Gateway Service
After=network.target

[Service]
Type=simple
WorkingDirectory=/home/ubuntu/orahermes-agent
ExecStart=/home/ubuntu/orahermes-agent/venv/bin/python -m gateway.run
Environment=PATH=/home/ubuntu/orahermes-agent/venv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
Environment=VIRTUAL_ENV=/home/ubuntu/orahermes-agent/venv
Environment=HERMES_HOME=/home/ubuntu/.hermes
EnvironmentFile=-/home/ubuntu/.hermes/.env
Restart=always
RestartSec=5
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=default.target
EOF

# Start and enable gateway
systemctl --user daemon-reload
systemctl --user enable hermes-gateway
systemctl --user start hermes-gateway
systemctl --user status hermes-gateway
```

Verify logs:
```bash
journalctl --user -u hermes-gateway -n 30 --no-pager
# Output should show: [Telegram] Connected to Telegram (polling mode)
```

---

## 9. Deploy OraHermes Web Dashboard Systemd Service

Create `/etc/systemd/system/hermes-dashboard.service`:

```ini
[Unit]
Description=OraHermes Agent Web Dashboard
After=network.target

[Service]
Type=simple
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu/orahermes-agent
ExecStart=/home/ubuntu/orahermes-agent/venv/bin/hermes dashboard --host 127.0.0.1 --port 8000 --no-open --skip-build
Environment=PATH=/home/ubuntu/orahermes-agent/venv/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
Environment=VIRTUAL_ENV=/home/ubuntu/orahermes-agent/venv
Environment=HERMES_HOME=/home/ubuntu/.hermes
EnvironmentFile=-/home/ubuntu/.hermes/.env
Restart=always
RestartSec=5
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

Enable and start:
```bash
sudo systemctl daemon-reload
sudo systemctl enable hermes-dashboard
sudo systemctl start hermes-dashboard
sudo systemctl status hermes-dashboard
```

---

## 10. Configure Nginx HTTPS Reverse Proxy with HTTP Basic Auth

### Step 1: Create HTTP Basic Auth File
```bash
sudo htpasswd -bc /etc/nginx/.htpasswd admin <your-dashboard-password>
sudo htpasswd -b /etc/nginx/.htpasswd ubuntu <your-dashboard-password>
sudo chmod 640 /etc/nginx/.htpasswd
sudo chown root:www-data /etc/nginx/.htpasswd
```

### Step 2: Create Self-Signed SSL Certificate
```bash
sudo mkdir -p /etc/nginx/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/nginx/ssl/dashboard.key \
  -out /etc/nginx/ssl/dashboard.crt \
  -subj "/C=PK/ST=State/L=City/O=JTCommunity/CN=<your-server-ip>"
```

### Step 3: Configure Site
Create `/etc/nginx/sites-available/orahermes-dashboard`:
```nginx
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name <your-server-ip> _;

    auth_basic "Restricted OraHermes Workspace";
    auth_basic_user_file /etc/nginx/.htpasswd;

    client_max_body_size 50M;

    location @handle_head {
        default_type text/html;
        return 200;
    }

    location / {
        proxy_intercept_errors on;
        error_page 405 =200 @handle_head;

        proxy_pass http://127.0.0.1:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header Host 127.0.0.1;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400s;
        proxy_send_timeout 86400s;
    }
}

server {
    listen 443 ssl http2 default_server;
    listen [::]:443 ssl http2 default_server;
    server_name <your-server-ip> _;

    ssl_certificate /etc/nginx/ssl/dashboard.crt;
    ssl_certificate_key /etc/nginx/ssl/dashboard.key;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    auth_basic "Restricted OraHermes Workspace";
    auth_basic_user_file /etc/nginx/.htpasswd;

    client_max_body_size 50M;

    location @handle_head {
        default_type text/html;
        return 200;
    }

    location / {
        proxy_intercept_errors on;
        error_page 405 =200 @handle_head;

        proxy_pass http://127.0.0.1:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header Host 127.0.0.1;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400s;
        proxy_send_timeout 86400s;
    }
}
```

Enable site:
```bash
sudo ln -sf /etc/nginx/sites-available/orahermes-dashboard /etc/nginx/sites-enabled/
sudo rm -f /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl restart nginx
```

---

## 11. Verification & Testing

### Test 1: Web Dashboard Authentication
- **Unauthenticated**:
  `curl.exe -k -s -I https://<your-server-ip>/` → Expected: `HTTP/1.1 401 Unauthorized`
- **Authenticated**:
  `curl.exe -k -s -u admin:<your-dashboard-password> -I https://<your-server-ip>/` → Expected: `HTTP/1.1 200 OK`

### Test 2: Telegram Bot Integration
1. Open `@jtcommunitybot` in Telegram.
2. Send `/start` or `Hello! Introduce yourself`.
3. Verify live response from `nvidia/nemotron-3-ultra-550b-a55b`.

---

## 12. Useful Management Commands

```bash
# Gateway status and logs
systemctl --user status hermes-gateway
journalctl --user -u hermes-gateway -n 50 --no-pager

# Dashboard status and logs
sudo systemctl status hermes-dashboard
journalctl -u hermes-dashboard -n 50 --no-pager

# Nginx management
sudo nginx -t
sudo systemctl reload nginx

# Resource inspection
free -h
df -h
```

---

## 13. Common Errors & Fixes

| Symptom | Cause | Resolution |
|---|---|---|
| Dashboard 401 | Incorrect credentials | Update with `sudo htpasswd -b /etc/nginx/.htpasswd admin <password>` |
| Dashboard 405 on HEAD | SPA router method mismatch | Use `@handle_head` block in Nginx configuration |
| FastAPI Host error | GHSA-ppp5-vxwm-4cf7 loopback check | Forward `Host 127.0.0.1;` from Nginx |
| Telegram bot silent | ID not whitelisted | Add numeric ID to `TELEGRAM_ALLOWED_USERS` in `.env` |
| Server freezes | Missing swap | Run Section 3 swap configuration commands |

---

*JT Community Production Deployment | OraHermes Agent*
