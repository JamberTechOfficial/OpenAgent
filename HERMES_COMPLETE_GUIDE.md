# 🤖 ORAHERMES AGENT — MUKAMMAL SETUP & ARCHITECTURE GUIDE (v3 — Production)
### Oracle Cloud (Ubuntu) • NVIDIA NIM AI • Telegram Bot Gateway • OraHermes Web Dashboard • Nginx HTTPS Auth
#### English • اردو • Roman Urdu

> [!IMPORTANT]
> This guide documents the **production-grade, tested installation and architecture** of `orahermes-agent` deployed on the JT Community Oracle Cloud infrastructure (Oct 2026).
> یہ گائیڈ JT Community سرور پر **orahermes-agent کی باقاعدہ اور آزمودہ تنصیب** پر مبنی ہے۔
> Yeh guide JT Community server par **orahermes-agent ki mukammal aur test ki hui installation** par mabni hai.

| Item | Value |
|---|---|
| Server IP | `<your-server-ip>` |
| User | `ubuntu` |
| OS | Ubuntu 20.04.6 LTS, 1 GB RAM, x86_64 (Oracle Always Free) |
| Architecture | Headless server (XRDP / XFCE4 purged for maximum RAM & disk efficiency) |
| Target Agent | `orahermes-agent` (Python 3.11+ via `uv` in `/home/ubuntu/orahermes-agent/venv`) |
| SSH Key | `<path-to-private-key>` |
| AI Model | `nvidia/nemotron-3-ultra-550b-a55b` (NVIDIA NIM) |
| Telegram Bot | `@jtcommunitybot` (token: `<telegram-bot-token>`, allowed user: `<telegram-user-id>`) |
| Messaging Gateway | `hermes-gateway.service` (Systemd User Service, polling mode) |
| Web Dashboard | `hermes-dashboard.service` (Systemd Service on `127.0.0.1:8000`) |
| Reverse Proxy | Nginx HTTPS reverse proxy on Port 443 & Port 80 with HTTP Basic Auth |
| Backup Archive | `/home/ubuntu/hermes_backup_20261029_075359/` |
| Public Ports | Port 22 (SSH key-only + fail2ban), Port 80/443 (Nginx Web Dashboard + HTTP Basic Auth) |

> [!CAUTION]
> **Never share your keys publicly.** All tokens, keys, passwords, and IP addresses in this guide use `<placeholders>`.
> اپنی keys اور passwords کبھی پبلک نہ کریں۔ | Apni keys aur passwords kabhi public na karein.

---

## 📋 Fehrist / فہرست / Contents

1. [Oracle Cloud par server banana](#step-1--oracle-cloud-par-server-banana)
2. [SSH se connect karna](#step-2--ssh-se-connect-karna)
3. [Swap memory add karna (bohat zaroori!)](#step-3--swap-memory-add-karna-bohat-zaroori)
4. [Headless Optimization: GUI & XRDP Purge](#step-4--headless-optimization-gui--xrdp-purge)
5. [Zaroori packages & Python 3.11 with `uv`](#step-5--zaroori-packages--python-311-with-uv)
6. [orahermes-agent clone & setup](#step-6--orahermes-agent-clone--setup)
7. [NVIDIA NIM API key & model set karna](#step-7--nvidia-nim-api-key--model-set-karna)
8. [Telegram bot banana & credentials](#step-8--telegram-bot-banana--credentials)
9. [Decommissioning & Backup Archive](#step-9--decommissioning--backup-archive)
10. [Dual Service Architecture: Gateway & Web Dashboard](#step-10--dual-service-architecture-gateway--web-dashboard)
11. [Nginx HTTPS Reverse Proxy with HTTP Basic Auth (Port 443)](#step-11--nginx-https-reverse-proxy-with-http-basic-auth-port-443)
12. [Security: Hardened SSH, fail2ban & Firewall](#step-12--security-hardened-ssh-fail2ban--firewall)
13. [Test karna & Verification](#step-13--test-karna--verification)
14. [Roz-marra ke commands](#step-14--roz-marra-ke-commands)
15. [Troubleshooting (asal masail jo pesh aaye)](#-troubleshooting--asal-masail-jo-pesh-aaye)

---

## STEP 1 — Oracle Cloud par server banana

### 🇬🇧 English
1. Go to `https://cloud.oracle.com` and create a free account (card required for identity verification only).
2. Menu → **Compute → Instances → Create instance**.
3. **Name:** e.g. `hermes-server`.
4. **Image:** *Canonical Ubuntu* (20.04 or 22.04 LTS).
5. **Shape:** `VM.Standard.E2.1.Micro` (Always Free, 1 GB RAM) — or **Ampere A1 (ARM)** with 2–4 GB RAM if available.
6. **Networking:** default VCN, **Assign a public IPv4 address = Yes**.
7. **SSH keys:** choose *Generate a key pair for me* → click **Save private key** (downloads `<your-key-name>.key` — keep it safe).
8. Click **Create**. Status becomes **RUNNING** after ~2 minutes — copy `<your-server-ip>`.

### 🇵🇰 اردو
1. https://cloud.oracle.com پر جائیں اور مفت اکاؤنٹ بنائیں (کارڈ صرف تصدیق کے لیے)۔
2. مینو ← **Compute ← Instances ← Create instance**۔
3. **نام:** مثلاً `hermes-server`۔
4. **Image:** *Canonical Ubuntu* (20.04 یا 22.04)۔
5. **Shape:** `VM.Standard.E2.1.Micro` (ہمیشہ مفت، 1 GB RAM) — یا **Ampere A1 (ARM)**۔
6. **Networking:** ڈیفالٹ VCN، **Public IPv4 address = Yes**۔
7. **SSH keys:** *Generate a key pair for me* ← **Save private key** دبائیں (`.key` فائل سنبھال کر رکھیں)۔
8. **Create** دبائیں۔ 2 منٹ بعد **RUNNING** ہونے پر `<your-server-ip>` کاپی کریں۔

### 🗣️ Roman Urdu
1. https://cloud.oracle.com par jayein aur free account banayein (card sirf verification ke liye).
2. Menu → **Compute → Instances → Create instance**.
3. **Naam:** maslan `hermes-server`.
4. **Image:** Canonical Ubuntu (20.04 ya 22.04).
5. **Shape:** `VM.Standard.E2.1.Micro` (hamesha free, 1 GB RAM) — ya Ampere A1 (ARM).
6. **Networking:** default VCN, **Public IPv4 address = Yes**.
7. **SSH keys:** *Generate a key pair for me* → **Save private key** dabayein.
8. **Create** dabayein. Status **RUNNING** hone par `<your-server-ip>` copy karein.

---

## STEP 2 — SSH se connect karna

### 🇬🇧 English
On Windows, open **PowerShell** and run:
```powershell
ssh -i "<path-to-private-key>" ubuntu@<your-server-ip>
```
Type `yes` the first time. If you receive an *"UNPROTECTED PRIVATE KEY FILE"* error, fix permissions once:
```powershell
icacls "<path-to-private-key>" /inheritance:r /grant:r "$($env:USERNAME):(R)"
```
On mobile you can use **Termius** or **JuiceSSH**: import your key file, host `<your-server-ip>`, user `ubuntu`.

### 🇵🇰 اردو
ونڈوز پر **PowerShell** کھولیں اور اوپر والی `ssh` کمانڈ چلائیں۔ پہلی بار `yes` لکھیں۔
اگر *"UNPROTECTED PRIVATE KEY FILE"* آئے تو اوپر والی `icacls` کمانڈ ایک بار چلائیں۔

### 🗣️ Roman Urdu
Windows par **PowerShell** kholen aur upar wali `ssh` command chalayein. Pehli baar `yes` likhein.
Agar *"UNPROTECTED PRIVATE KEY FILE"* aaye to upar wali `icacls` command ek dafa chalayein.

---

## STEP 3 — Swap memory add karna (bohat zaroori!)

> [!WARNING]
> **EN:** The Always Free micro instance has only 1 GB RAM and no default swap. Without swap, Python package installs or AI token buffering can exhaust RAM and cause kernel panic / lockup. Adding 4 GB swap ensures complete stability.
> **اردو:** مفت سرور میں صرف 1 GB RAM ہے اور swap نہیں ہوتی۔ Swap کے بغیر سرور جام ہو سکتا ہے۔ 4 GB swap بنانا لازمی ہے۔
> **Roman:** Free server mein sirf 1 GB RAM hoti hai aur swap nahi. Swap na ho to server hang ho jata hai. 4 GB swap lazmi banayein.

```bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
free -h        # Confirm: "Swap: 4.0Gi"
```

---

## STEP 4 — Headless Optimization: GUI & XRDP Purge

> [!TIP]
> **EN:** Desktop environments (XFCE, GNOME, XRDP) consume up to 400 MB of RAM and unnecessary disk space. Purging them leaves 800+ MB of RAM free for the AI agent, Telegram gateway, and Web Dashboard.
> **اردو:** XRDP اور گرافیکل ڈیسک ٹاپ ہٹانے سے قیمتی RAM اور ڈسک آزاد ہوتی ہے جس سے ایجنٹ انتہائی تیز اور مستحکم چلتا ہے۔
> **Roman:** XRDP aur GUI khatam karne se server ki RAM free ho jati hai aur agent bina kisi rukawat ke fast chalta hai.

```bash
# 1. Stop and disable legacy display and RDP services
sudo systemctl stop xrdp xrdp-sesman lightdm gdm3 || true
sudo systemctl disable xrdp xrdp-sesman lightdm gdm3 || true

# 2. Purge desktop and Xorg packages
sudo DEBIAN_FRONTEND=noninteractive apt-get purge -y xrdp xorg 'xfce4*' 'lightdm*' 'gdm3*' 'xserver*' xorg-docs-core
sudo DEBIAN_FRONTEND=noninteractive apt-get autoremove -y --purge
sudo apt-get clean

# 3. Clean legacy NAT redirect rules (e.g. 443 -> 3389)
sudo iptables -t nat -D PREROUTING 1 2>/dev/null || true
sudo netfilter-persistent save
```

---

## STEP 5 — Zaroori packages & Python 3.11 with `uv`

`orahermes-agent` requires Python 3.11+ and fast package management via `uv`:

```bash
# Update repositories and install foundational tools
sudo apt-get update -y
sudo apt-get install -y git curl fail2ban libatomic1 software-properties-common nginx apache2-utils

# Add deadsnakes PPA for Python 3.11
sudo add-apt-repository -y ppa:deadsnakes/ppa
sudo apt-get update -y
sudo apt-get install -y python3.11 python3.11-venv python3.11-dev

# Install astral uv (blazing fast Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.cargo/env
```

---

## STEP 6 — orahermes-agent clone & setup

```bash
# Clone the repository
cd ~
git clone https://github.com/jasperan/orahermes-agent.git
cd ~/orahermes-agent

# Create virtual environment with Python 3.11
uv venv venv --python python3.11
source venv/bin/activate

# Install dependencies and editable package
uv pip install -e .
```

Verify the CLI binary:
```bash
~/orahermes-agent/venv/bin/hermes --version
```

---

## STEP 7 — NVIDIA NIM API key & model set karna

1. Open `https://build.nvidia.com` and generate your API key (format: `<nvidia-api-key>`).
2. Add your credentials to `~/.hermes/.env`:

```bash
mkdir -p ~/.hermes
cat > ~/.hermes/.env << 'EOF'
NVIDIA_API_KEY=<nvidia-api-key>
TELEGRAM_BOT_TOKEN=<telegram-bot-token>
TELEGRAM_ALLOWED_USERS=<telegram-user-id>
EOF
chmod 600 ~/.hermes/.env
```

Configure `config.yaml` to point to NVIDIA NIM:
```bash
~/orahermes-agent/venv/bin/hermes config set model.provider nvidia
~/orahermes-agent/venv/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1
~/orahermes-agent/venv/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

Tested models on NVIDIA NIM free tier:
| Model | Status | Speed | Notes |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ✅ Working | ~2s | **Production Default** (Tool calling enabled) |
| `minimaxai/minimax-m3.1-flash` | ✅ Working | ~2s | Excellent fast backup |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ✅ Working | ~2s | Small & lightweight |
| `z-ai/glm-5.3` | ✅ Working | ~55s | Functional but slower |

---

## STEP 8 — Telegram bot banana & credentials

1. In Telegram, chat with **@BotFather** and send `/newbot`.
2. Follow prompts to name your bot and choose a username ending in `bot` (e.g. `jtcommunitybot`).
3. Copy the token: `<telegram-bot-token>`.
4. Chat with **@userinfobot** to get your numeric User ID: `<telegram-user-id>`.
5. Ensure these are set in `~/.hermes/.env`.

---

## STEP 9 — Decommissioning & Backup Archive

When migrating from legacy installations, existing databases (`state.db`, `kanban.db`), configs, and logs are safely backed up before decommission:

- **Backup Archive Path:** `/home/ubuntu/hermes_backup_20261029_075359/`
- Contains:
  - `config/` (`.env`, `config.yaml`, `SOUL.md`)
  - `data/` (`state.db`, `kanban.db`, SQLite memory tables)
  - `skills/` (Custom local skills)
  - `service/` (`hermes-gateway.service` unit definition)

---

## STEP 10 — Dual Service Architecture: Gateway & Web Dashboard

`orahermes-agent` features a high-performance **dual service architecture**:

```
                              [Internet User]
                                     │
           ┌─────────────────────────┴─────────────────────────┐
           ▼ (HTTPS / Port 443 with HTTP Basic Auth)           ▼ (Outgoing Telegram Polling)
   [Nginx Reverse Proxy]                                [hermes-gateway.service]
           │                                                   │
           ▼ (127.0.0.1:8000)                                  │
[hermes-dashboard.service]                                     ▼
(Sessions, Logs, Cron, Skills, Config)               [Telegram Bot API Servers]
```

### 1. Telegram Messaging Gateway (`hermes-gateway.service`)
Configured as a systemd user service with linger enabled:
```bash
sudo loginctl enable-linger ubuntu
systemctl --user daemon-reload
systemctl --user enable hermes-gateway
systemctl --user start hermes-gateway
systemctl --user status hermes-gateway
```
Check live polling logs:
```bash
journalctl --user -u hermes-gateway -f
# Expected: [Telegram] Connected to Telegram (polling mode)
```

### 2. OraHermes Web Dashboard (`hermes-dashboard.service`)
Configured as a system-level service running the FastAPI / Vue SPA dashboard:
File: `/etc/systemd/system/hermes-dashboard.service`
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
Manage dashboard service:
```bash
sudo systemctl daemon-reload
sudo systemctl enable hermes-dashboard
sudo systemctl start hermes-dashboard
sudo systemctl status hermes-dashboard
```

---

## STEP 11 — Nginx HTTPS Reverse Proxy with HTTP Basic Auth (Port 443)

To expose the OraHermes Web Dashboard securely without public unauthorized access, Nginx provides SSL termination and HTTP Basic Auth.

### 1. Create HTTP Basic Auth Credentials
```bash
sudo htpasswd -bc /etc/nginx/.htpasswd admin <dashboard-password>
sudo htpasswd -b /etc/nginx/.htpasswd ubuntu <dashboard-password>
sudo chmod 640 /etc/nginx/.htpasswd
sudo chown root:www-data /etc/nginx/.htpasswd
```

### 2. SSL Certificate Generation
```bash
sudo mkdir -p /etc/nginx/ssl
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/nginx/ssl/dashboard.key \
  -out /etc/nginx/ssl/dashboard.crt \
  -subj "/C=PK/ST=State/L=City/O=JTCommunity/CN=<your-server-ip>"
```

### 3. Nginx Site Configuration (`/etc/nginx/sites-available/orahermes-dashboard`)
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

Enable site and restart Nginx:
```bash
sudo ln -sf /etc/nginx/sites-available/orahermes-dashboard /etc/nginx/sites-enabled/
sudo rm -f /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl restart nginx
```

---

## STEP 12 — Security: Hardened SSH, fail2ban & Firewall

1. **SSH Hardening**:
   ```bash
   sudo tee /etc/ssh/sshd_config.d/99-hardening.conf >/dev/null <<'EOF'
   PasswordAuthentication no
   PermitRootLogin no
   MaxAuthTries 3
   EOF
   sudo sshd -t && sudo systemctl reload ssh
   ```

2. **fail2ban Protection**:
   ```bash
   sudo tee /etc/fail2ban/jail.d/sshd.local >/dev/null <<'EOF'
   [sshd]
   enabled = true
   maxretry = 4
   findtime = 10m
   bantime = 1h
   EOF
   sudo systemctl restart fail2ban
   ```

3. **Firewall (IPTables)**:
   Allow incoming traffic on ports 22 (SSH), 80 (HTTP), and 443 (HTTPS) only.

---

## STEP 13 — Test karna & Verification

### 1. Web Dashboard Verification
- **Unauthenticated Check (Must return 401 Unauthorized)**:
  ```powershell
  curl.exe -k -s -I https://<your-server-ip>/
  # HTTP/1.1 401 Unauthorized
  ```
- **Authenticated Check (Returns 200 OK & Loads Dashboard)**:
  ```powershell
  curl.exe -k -s -u admin:<dashboard-password> -I https://<your-server-ip>/
  # HTTP/1.1 200 OK
  ```
- Open in your browser: `https://<your-server-ip>/`. Accept the self-signed certificate and log in with user `admin` and `<dashboard-password>`.

### 2. Telegram Bot Verification
1. In Telegram, open `@jtcommunitybot`.
2. Tap **START**.
3. Send: `Assalam o Alaikum, introduce yourself`.
4. Verify response generated via `nvidia/nemotron-3-ultra-550b-a55b`.

---

## STEP 14 — Roz-marra ke commands

| Task | Command |
|---|---|
| Connect via SSH | `ssh -i "<path-to-private-key>" ubuntu@<your-server-ip>` |
| Gateway Status | `systemctl --user status hermes-gateway` |
| Gateway Restart | `systemctl --user restart hermes-gateway` |
| Gateway Live Logs | `journalctl --user -u hermes-gateway -f` |
| Dashboard Status | `sudo systemctl status hermes-dashboard` |
| Dashboard Restart | `sudo systemctl restart hermes-dashboard` |
| Dashboard Logs | `journalctl -u hermes-dashboard -n 50 --no-pager` |
| Nginx Status / Test | `sudo systemctl status nginx` / `sudo nginx -t` |
| Memory / Swap Check | `free -h` |
| Fail2ban Status | `sudo fail2ban-client status sshd` |

---

## 🔧 Troubleshooting — asal masail jo pesh aaye

1. **Dashboard returns 401 Unauthorized**:
   - Verify username (`admin` or `ubuntu`) and password match the entries in `/etc/nginx/.htpasswd`.
2. **Dashboard returns 405 Method Not Allowed on HEAD**:
   - Nginx configuration includes `@handle_head` to intercept HEAD requests and return 200 OK.
3. **Loopback Host Check failure in FastAPI**:
   - OraHermes agent security middleware expects `Host: 127.0.0.1`. Nginx handles this with `proxy_set_header Host 127.0.0.1;`.
4. **Telegram bot doesn't reply**:
   - Check `journalctl --user -u hermes-gateway -n 50 --no-pager`. Verify `TELEGRAM_ALLOWED_USERS` contains your user ID.
5. **Memory exhaust on 1 GB VPS**:
   - Verify swap is active with `swapon --show`. Ensure XRDP and GUI desktop packages are purged.

---

*Production Release v3.0 | OraHermes Agent for JT Community | Oct 2026*
