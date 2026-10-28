# 02 — Free Server Alternatives for Hosting AI Agents / Bots

---

## 1. Introduction

When **Oracle Cloud** doesn't work (card issues, regional capacity problems, etc.), there are several excellent free alternatives to host your AI agents and bots. This document covers every major option, their limits, and exactly how to deploy **Hermes** on them.

---

## 2. Comparison Table

| Platform | Free RAM | CPU | Storage | Sleep? | Card Required? | Best For |
|---|---|---|---|---|---|---|
| **Oracle Cloud** | 24 GB (ARM) | 4 vCPU | 200 GB | ❌ No | ✅ Yes (not charged) | Best overall free VPS |
| **Google Cloud** | 1 GB (e2-micro) | 0.25 vCPU | 30 GB | ❌ No | ✅ Yes | Reliable, US only |
| **AWS Free Tier** | 1 GB (t3.micro) | 2 vCPU | 30 GB | ❌ No | ✅ Yes | 12 months only |
| **Azure Free** | 1 GB (B1S) | 1 vCPU | 64 GB | ❌ No | ✅ Yes | 12 months only |
| **Render** | 512 MB | Shared | 1 GB | ⚠️ YES (15 min) | ❌ No | Simple web apps |
| **Railway** | 512 MB | Shared | 1 GB | ❌ No (with \$5 credit) | ❌ No | Easiest deployment |
| **Fly.io** | 256 MB | Shared | 3 GB | ⚠️ After inactivity | ❌ No | Containers |
| **Koyeb** | 512 MB | 0.1 vCPU | — | ❌ No | ❌ No | European free tier |
| **Deta Space** | — | — | 10 GB | ❌ No | ❌ No | Python apps |

---

## 3. Platform Details

### 🏆 Oracle Cloud Always Free (BEST)

- **2× AMD micro** VMs **OR** **4× Ampere A1 ARM** (up to 24 GB RAM!)
- Truly **permanent** — never expires
- Full **root access**, systemd, Docker — everything works
- 200 GB block storage included
- ⚠️ **Problem:** Hard to sign up — card verification is strict
- ✅ **Solution:** Use a **physical credit card** from a major bank (Meezan, HBL, UBL international). Enable international transactions first.
- 🔗 https://cloud.oracle.com

---

### Google Cloud Free Tier

- **e2-micro** instance in **us-central1** or **us-east1 ONLY** — other regions cost money!
- Always free, **no expiry**
- 1 shared vCPU, 1 GB RAM — enough for a Telegram bot
- 30 GB standard persistent disk
- 1 GB egress data transfer/month (US to US)
- Requires credit card but **free tier will NOT be charged**
- 🔗 https://cloud.google.com

**Steps to create:**
1. Create Google account → go to https://cloud.google.com
2. Start free trial (enter card — won't be charged on free tier)
3. Go to **Compute Engine** → **VM Instances** → **Create Instance**
4. Choose **e2-micro** machine type
5. Region: **us-central1** or **us-east1**
6. Boot disk: **Ubuntu 22.04 LTS**, 30 GB
7. Click **Create** → wait → click **SSH**

---

### AWS Free Tier

- **t2.micro** or **t3.micro**: 1 GB RAM, 2 vCPU
- ⚠️ **12 months only** — then charges start automatically!
- 30 GB EBS storage, 15 GB data transfer/month
- Good for learning but **set billing alerts immediately!**
- 🔗 https://aws.amazon.com/free

> **Warning:** AWS will charge after 12 months if you don't shut down instances. Always set a billing alert at \$1 to avoid surprises.

---

### Azure Free

- **B1S**: 1 vCPU, 1 GB RAM
- ⚠️ **12 months free** then charges begin
- 64 GB storage (better than AWS!)
- \$200 credit for first 30 days
- 🔗 https://azure.microsoft.com/free

> **Warning:** Same as AWS — set spending limits in Azure Cost Management.

---

### Render (No card needed! ⚠️ Sleeps!)

- 512 MB RAM, shared CPU
- ⚠️ **Sleeps after 15 minutes of inactivity** — **bad for bots that must receive messages 24/7**
- Free tier: **750 hours/month** (enough for 1 service running all month)
- **Workaround for sleep:** Use [UptimeRobot](https://uptimerobot.com) — ping your service URL every **14 minutes** to keep it awake (free plan available)
- Deploy: Connect GitHub repo → Render auto-deploys
- 🔗 https://render.com

---

### Railway (Easiest! ⭐ Recommended for beginners)

- **\$5 free credit per month** — no card needed
- 512 MB RAM, shared CPU
- **No sleep** — runs continuously
- Deploy via GitHub or Docker
- Great dashboard, easy environment variable management
- 🔗 https://railway.app

> **Note:** \$5/month is enough for a lightweight bot. If your bot uses heavy AI inference, it may run out mid-month.

---

### Fly.io

- **3 shared-cpu-1x VMs** free (256 MB RAM each)
- Apps sleep after inactivity but **wake up on incoming request**
- Deploy via **Docker** (`flyctl deploy`)
- Good for containerized apps
- 🔗 https://fly.io

---

### Koyeb

- European platform (servers in Frankfurt, Paris)
- **512 MB RAM, 0.1 vCPU** free
- **No card required**
- No sleep (always on)
- Good for EU-based bots
- 🔗 https://koyeb.com

---

### Deta Space

- Python-focused platform
- 10 GB storage
- No card required
- Good for simple Python apps and webhooks
- 🔗 https://deta.space

---

## 4. Recommendation by Use Case

### For a Telegram Bot (like Hermes):

| Priority | Platform | Why |
|---|---|---|
| 🥇 **Best** | Oracle Cloud ARM A1 | 24 GB RAM, permanent, root access |
| 🥈 **Second Best** | Google Cloud e2-micro | 1 GB RAM, permanent, US only |
| 🥉 **No Card Option** | Railway | \$5 credit/month, no sleep, easy |
| 🆓 **No Card, EU** | Koyeb | Always on, European servers |
| ⚠️ **Avoid** | Render | Bot sleeps = misses messages |

---

## 5. What Specs Does Hermes Agent Need?

| Resource | Minimum | Recommended | Ideal |
|---|---|---|---|
| **RAM** | 1 GB + 2 GB swap | 2 GB | 4+ GB (Oracle A1!) |
| **CPU** | 1 vCPU | 2 vCPU | 4 vCPU |
| **Disk** | 5 GB | 10 GB | 20+ GB |
| **OS** | Ubuntu 20.04 | Ubuntu 22.04 LTS | Ubuntu 22.04 LTS |
| **Network** | Any | Any | Low-latency |

### How to Add Swap (if RAM is low):

```bash
# Add 2 GB swap on any Linux server
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Make it permanent
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Verify
free -h
```

---

## 6. How to Deploy Hermes on Render

> ⚠️ **Warning:** Render's free tier sleeps after 15 minutes of inactivity. Your bot **will miss Telegram messages** while asleep. Use the UptimeRobot workaround described below.

### Step-by-Step:

**Step 1 — Prepare your repo**
```
your-repo/
├── main.py           # Hermes bot entry point
├── requirements.txt  # All dependencies
├── .env              # DO NOT commit this!
└── render.yaml       # (optional) Render config
```

**Step 2 — Push to GitHub**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/hermes-bot
git push -u origin main
```

**Step 3 — Create Render account**
- Go to https://render.com → Sign up (no card needed)
- Click **New +** → **Web Service**
- Connect your GitHub account → Select your repo

**Step 4 — Configure the service**
```
Name:        hermes-bot
Environment: Python 3
Build Command: pip install -r requirements.txt
Start Command: python main.py
Instance Type: Free
```

**Step 5 — Add environment variables**
- In Render dashboard → **Environment** tab
- Add: `BOT_TOKEN`, `OPENAI_API_KEY`, etc.
- Click **Save Changes**

**Step 6 — Deploy**
- Click **Deploy** — Render builds and starts your bot
- Check **Logs** tab for any errors

**Step 7 — Fix sleep issue with UptimeRobot**
```
1. Add a health-check endpoint to your bot:
   @app.get("/health")
   def health(): return {"status": "ok"}

2. Go to https://uptimerobot.com → Sign up (free)
3. New Monitor → HTTP(s) → Your Render URL + /health
4. Interval: 14 minutes
5. Save — your bot now stays awake!
```

---

## 7. How to Deploy Hermes on Google Cloud (Step by Step)

This is the **recommended free alternative** — permanent, 1 GB RAM, no sleep.

### Step 1 — Create Google Cloud Account

1. Go to https://cloud.google.com
2. Click **Get started for free**
3. Sign in with Google account
4. Enter billing info (card required — **you will NOT be charged on free tier**)
5. You get \$300 credit for 90 days + permanent free tier after

### Step 2 — Enable Compute Engine

1. In Google Cloud Console → search **"Compute Engine"**
2. Click **Enable** (may take 1–2 minutes)

### Step 3 — Create VM Instance

1. Go to **Compute Engine** → **VM Instances** → **Create Instance**
2. Configure:

```
Name:         hermes-server
Region:       us-central1   ← MUST be this or us-east1
Zone:         us-central1-a
Machine type: e2-micro       ← This is the free one!
Boot disk:    Ubuntu 22.04 LTS, 30 GB Standard
Firewall:     ✅ Allow HTTP traffic
              ✅ Allow HTTPS traffic
```

3. Click **Create**

### Step 4 — Connect via SSH

```bash
# In Google Cloud Console, click SSH button next to your VM
# OR use gcloud CLI:
gcloud compute ssh hermes-server --zone=us-central1-a
```

### Step 5 — Install Dependencies

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Python and pip
sudo apt install python3 python3-pip python3-venv git -y

# Add swap (important for 1 GB RAM!)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

### Step 6 — Clone and Set Up Hermes

```bash
# Clone your Hermes repo
git clone https://github.com/yourusername/hermes-bot.git
cd hermes-bot

# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install requirements
pip install -r requirements.txt

# Create .env file
nano .env
# Add: BOT_TOKEN=your_token_here
# Add: OPENAI_API_KEY=your_key_here
# Save: Ctrl+X → Y → Enter
```

### Step 7 — Run as a systemd Service (Auto-restart!)

```bash
# Create service file
sudo nano /etc/systemd/system/hermes.service
```

Paste this content:
```ini
[Unit]
Description=Hermes Telegram Bot
After=network.target

[Service]
Type=simple
User=YOUR_USERNAME
WorkingDirectory=/home/YOUR_USERNAME/hermes-bot
ExecStart=/home/YOUR_USERNAME/hermes-bot/venv/bin/python main.py
Restart=always
RestartSec=10
EnvironmentFile=/home/YOUR_USERNAME/hermes-bot/.env

[Install]
WantedBy=multi-user.target
```

```bash
# Enable and start
sudo systemctl daemon-reload
sudo systemctl enable hermes
sudo systemctl start hermes

# Check status
sudo systemctl status hermes

# View logs
sudo journalctl -u hermes -f
```

### Step 8 — Verify it's Running

```bash
# Check if bot process is running
ps aux | grep python

# Check logs
sudo journalctl -u hermes --since "10 minutes ago"
```

✅ **Done!** Hermes is now running 24/7 on Google Cloud for free.

---

## Quick Reference Card

```
╔══════════════════════════════════════════════════════════════╗
║           HERMES BOT — FREE HOSTING QUICK GUIDE             ║
╠══════════════════════════════════════════════════════════════╣
║  BEST:        Oracle Cloud A1  → 24 GB RAM, free forever    ║
║  SECOND:      Google Cloud     → 1 GB RAM, us-central1      ║
║  NO CARD:     Railway          → $5/mo credit, no sleep     ║
║  EU / NO CARD:Koyeb            → 512 MB, always on          ║
║  AVOID:       Render           → sleeps, misses messages     ║
╠══════════════════════════════════════════════════════════════╣
║  Hermes Min Specs: 1 GB RAM + 2 GB swap, 5 GB disk           ║
║  Best OS: Ubuntu 22.04 LTS                                   ║
║  Always set up: systemd auto-restart + swap                  ║
╚══════════════════════════════════════════════════════════════╝
```

---

*Last updated: 2025 | Maintained by JT Community*
