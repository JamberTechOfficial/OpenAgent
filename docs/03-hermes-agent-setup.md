# 03 — Hermes Agent Setup

> **Status:** ✅ Tested on Oracle Cloud Ubuntu 20.04 | AMD 1 vCPU Micro | 1 GB RAM
> **Version Tested:** `hermes v0.22.5` with Python 3.14.9

---

## Table of Contents

1. [What is Hermes Agent?](#1-what-is-hermes-agent)
2. [Prerequisites](#2-prerequisites)
3. [⚠️ CRITICAL: Add Swap BEFORE Installing](#3-️-critical-add-swap-before-installing-tested-)
4. [Install Prerequisites](#4-install-prerequisites-tested-)
5. [Install Hermes](#5-install-hermes-tested-)
6. [Configure Credentials](#6-configure-credentials-tested-)
7. [Configure Model](#7-configure-model-tested-)
8. [NVIDIA Models That Work](#8-nvidia-models-that-work-tested-)
9. [Install Telegram Gateway as System Service](#9-install-telegram-gateway-as-system-service-tested-)
10. [Test the Bot](#10-test-the-bot)
11. [Useful Commands](#11-useful-commands-tested-)
12. [Security Hardening](#12-security-hardening-tested-)
13. [Common Errors & Fixes](#13-common-errors--fixes)
14. [Warnings / Harmless Messages](#14-warnings--harmless-messages)

---

## 1. What is Hermes Agent?

**Hermes Agent** is an open-source AI agent made by **NousResearch**. It can be used via:
- **Telegram** (chat with it like a bot)
- **CLI** (command line interface)
- **API** (programmatic access)

It connects to **NVIDIA NIM API** (free tier available) to run powerful AI models without needing a local GPU.

- 🔗 GitHub: [https://github.com/NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)
- 🔗 Install script: `https://install.hermes.sh`

---

## 2. Prerequisites

Before installing Hermes, you **NEED** the following. Each has its own setup guide:

| Requirement | Where to Get It | Guide |
|---|---|---|
| Ubuntu 20.04/22.04 Server | Oracle Cloud (free) | `01-oracle-cloud-setup.md` |
| NVIDIA API Key | [build.nvidia.com](https://build.nvidia.com) | `02-nvidia-nim-api.md` |
| Telegram Bot Token | Chat with [@BotFather](https://t.me/BotFather) on Telegram | Below |
| Your Telegram User ID | Chat with [@userinfobot](https://t.me/userinfobot) on Telegram | Below |

#### Getting your Telegram Bot Token
1. Open Telegram → search `@BotFather`
2. Send `/newbot`
3. Follow prompts, name your bot
4. BotFather gives you a token like: `1234567890:ABCdef...`  
   → This is your `<your-bot-token>`

#### Getting your Telegram User ID
1. Open Telegram → search `@userinfobot`
2. Send `/start`
3. It replies with your numeric ID like: `987654321`  
   → This is your `<your-telegram-user-id>`

---

## 3. ⚠️ CRITICAL: Add Swap BEFORE Installing (TESTED ✅)

> [!CAUTION]
> On servers with **1 GB RAM**, you **MUST** add swap memory before installing Hermes. Without it, the server **will freeze** during installation. This was confirmed in testing — the server completely locked up.

```bash
# Step 1: Check existing swap (usually none on fresh Oracle Cloud)
free -h
swapon --show

# Step 2: Create a 4 GB swap file
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Step 3: Make it permanent (survives reboots)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Step 4: Verify swap is active
free -h
# You should now see ~4 GB under "Swap:"
```

**Expected output after `free -h`:**
```
              total        used        free      shared  buff/cache   available
Mem:          969Mi       ...
Swap:         4.0Gi         0B       4.0Gi
```

---

## 4. Install Prerequisites (TESTED ✅)

Install the required system packages first:

```bash
sudo apt-get update
sudo apt-get install -y git curl screen libatomic1 fail2ban
```

| Package | Why It's Needed |
|---|---|
| `git` | General version control, may be needed by install |
| `curl` | Downloads the Hermes install script |
| `screen` | Run commands in background sessions (optional but useful) |
| `libatomic1` | **Required** by the Hermes binary — without it you get `libatomic.so.1 not found` error |
| `fail2ban` | Security: blocks brute-force SSH attacks automatically |

---

## 5. Install Hermes (TESTED ✅)

#### Method 1 — Direct Install (Standard)

```bash
curl -fsSL https://install.hermes.sh | bash
```

#### Method 2 — Via Script File (If Stdin Issues Occur)

If you get errors related to stdin/terminal input, use this workaround:

```bash
cat > /tmp/run_install.sh << 'EOF'
#!/bin/bash
curl -fsSL https://install.hermes.sh | bash
EOF
chmod +x /tmp/run_install.sh
/tmp/run_install.sh
```

#### After Installation

```bash
# Reload your shell profile so the new PATH takes effect
source ~/.bashrc

# Verify Hermes is installed
~/.local/bin/hermes --version
# Expected: hermes v0.22.5
```

> [!NOTE]
> The install places the binary at `~/.local/bin/hermes`. If `hermes` still isn't found after `source ~/.bashrc`, always use the full path `~/.local/bin/hermes`.

---

## 6. Configure Credentials (TESTED ✅)

> [!IMPORTANT]
> Replace the placeholders below with your **actual** values. Never share this file publicly.

```bash
# Create the Hermes config directory
mkdir -p ~/.hermes

# Write credentials to the env file
cat > ~/.hermes/.env << 'EOF'
NVIDIA_API_KEY=<your-nvidia-api-key>
TELEGRAM_BOT_TOKEN=<your-bot-token>
TELEGRAM_ALLOWED_USERS=<your-telegram-user-id>
EOF

# Restrict permissions so only your user can read it
chmod 600 ~/.hermes/.env
```

| Variable | Where to Find It |
|---|---|
| `NVIDIA_API_KEY` | From [build.nvidia.com](https://build.nvidia.com) → see `02-nvidia-nim-api.md` |
| `TELEGRAM_BOT_TOKEN` | From @BotFather → looks like `1234567890:ABCdef...` |
| `TELEGRAM_ALLOWED_USERS` | From @userinfobot → numeric ID like `987654321` |

> [!TIP]
> `TELEGRAM_ALLOWED_USERS` restricts who can use your bot. Only users whose IDs are listed here can interact with it. This is important for security.

---

## 7. Configure Model (TESTED ✅)

Tell Hermes to use the NVIDIA NIM API and set the default model:

```bash
# Set the AI provider to NVIDIA
~/.local/bin/hermes config set model.provider nvidia

# Set the NVIDIA NIM API base URL
~/.local/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1

# Set the default model (best tested option)
~/.local/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

> [!NOTE]
> These settings are saved to Hermes's config file (typically `~/.hermes/config.toml` or similar). You only need to run these once.

---

## 8. NVIDIA Models That Work (TESTED ✅)

The following models were tested against the **NVIDIA NIM free API**. Results may vary based on your account tier.

| Model | Speed | Tool Support | Status |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ~2s | ✅ Yes | ✅ **WORKS — IN USE** |
| `minimaxai/minimax-m3.1-flash` | ~2s | ✅ Yes | ✅ WORKS |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ~2s | ✅ Yes | ✅ WORKS |
| `z-ai/glm-5.3` | ~55s | ✅ Yes | ✅ WORKS (SLOW) |
| `nvidia/nemotron-3-super-120b-a12b` | — | — | ❌ 404 Not Found |
| `moonshotai/kimi-k2.6` | — | — | ❌ 404 Not Found |
| `deepseek-ai/deepseek-v4.1-flash` | — | — | ❌ Timeout |

> [!TIP]
> **Recommended:** Use `nvidia/nemotron-3-ultra-550b-a55b` — it's fast (~2s), supports tools, and is confirmed working on the free tier.

To switch models on the fly:
```bash
~/.local/bin/hermes config set model.default minimaxai/minimax-m3.1-flash
```

---

## 9. Install Telegram Gateway as System Service (TESTED ✅)

The Telegram gateway runs as a **user-level systemd service** so it starts automatically on boot and restarts if it crashes.

```bash
# Step 1: Install the gateway service
~/.local/bin/hermes gateway install

# Step 2: Start the gateway
~/.local/bin/hermes gateway start

# Step 3: Enable auto-start on reboot
# (This allows user services to run without being logged in)
loginctl enable-linger ubuntu

# Step 4: Check gateway status
~/.local/bin/hermes gateway status

# Step 5: View live logs (press Ctrl+C to stop)
journalctl --user -u hermes-gateway -f
```

**Expected log output (healthy gateway):**
```
[Telegram] Connected to Telegram (polling mode)
[Gateway] Listening for messages...
```

> [!NOTE]
> On a 1 GB RAM server, you may see `Gateway starting: deadline` in the status output. This is **normal** — the server is just slow to report. Test it by sending a message from Telegram.

---

## 10. Test the Bot

> [!IMPORTANT]
> The bot **CANNOT** message you first. You must always initiate the conversation.

**Steps to test:**
1. Open Telegram on your phone or desktop
2. Search for your bot by username (e.g., `@YourBotUsername`)
3. Tap **START** (very important — without this, the bot can't see you)
4. Type any message, e.g.: `Hello! What can you do?`
5. Wait a few seconds — the bot should reply

**If the bot doesn't reply:**
```bash
# Check the last 50 log lines for errors
journalctl --user -u hermes-gateway -n 50 --no-pager
```

Common reasons for no reply:
- You haven't pressed **START** yet
- The gateway isn't running (`hermes gateway status`)
- Your Telegram user ID isn't in `TELEGRAM_ALLOWED_USERS`
- Wrong bot token in `.env` file

---

## 11. Useful Commands (TESTED ✅)

```bash
# ── Gateway Management ──────────────────────────────────────────

# Check if gateway is running
~/.local/bin/hermes gateway status

# Start the gateway
~/.local/bin/hermes gateway start

# Restart the gateway (apply config changes)
~/.local/bin/hermes gateway restart

# Stop the gateway
~/.local/bin/hermes gateway stop

# ── Logs ────────────────────────────────────────────────────────

# View last 20 log lines
journalctl --user -u hermes-gateway -n 20 --no-pager

# Follow live logs
journalctl --user -u hermes-gateway -f

# View last 50 lines (for debugging)
journalctl --user -u hermes-gateway -n 50 --no-pager

# ── System Resources ─────────────────────────────────────────────

# Check RAM and swap usage
free -h

# Check disk space
df -h

# Live process monitor (press q to quit)
top
```

---

## 12. Security Hardening (TESTED ✅)

> [!CAUTION]
> **Disable password SSH before doing this** or you may lock yourself out. Make sure your SSH key is working first.

#### SSH Hardening

```bash
# Disable password login, root login; limit auth attempts
sudo bash -c 'cat > /etc/ssh/sshd_config.d/99-hardening.conf << EOF
PasswordAuthentication no
PermitRootLogin no
MaxAuthTries 3
EOF'

# Apply the new SSH config
sudo systemctl restart ssh
```

#### Fail2ban Configuration

```bash
# Configure fail2ban for SSH protection
sudo bash -c 'cat > /etc/fail2ban/jail.local << EOF
[sshd]
enabled = true
maxretry = 4
bantime = 3600
EOF'

# Restart fail2ban and verify it's watching SSH
sudo systemctl restart fail2ban
sudo fail2ban-client status sshd
```

**Expected output:**
```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  `- Total failed: 0
`- Actions
   |- Currently banned: 0
   `- Total banned: 0
```

> [!WARNING]
> **Never run `pkill -f hermes`** — the pattern may match your SSH session command and disconnect you. Instead, use:
> ```bash
> # Find the exact PID safely
> pgrep -af hermes
> # Then kill only that PID
> kill <PID>
> ```
> Or use `~/.local/bin/hermes gateway stop` which is safe.

---

## 13. Common Errors & Fixes

| Error / Symptom | Cause | Fix |
|---|---|---|
| Server froze during install | 1 GB RAM, no swap | ⚠️ Add 4 GB swap **BEFORE** install (Section 3) |
| `libatomic.so.1 not found` | Missing library | `sudo apt install libatomic1` |
| `hermes: command not found` | PATH not updated | `source ~/.bashrc` or use `~/.local/bin/hermes` |
| `Gateway starting: deadline` | Slow startup on 1 GB server | Normal — test via Telegram instead |
| Bot doesn't reply | User hasn't pressed START | Open bot in Telegram → press **START** first |
| `Chat not found` error | User never initiated | User must message bot first |
| Model 404 error | Model not available on free tier | Switch to `nvidia/nemotron-3-ultra-550b-a55b` |
| Model timeout | Model overloaded or unavailable | Retry, or switch to `minimax-m3.1-flash` |
| `pkill -f` disconnected SSH | Pattern too broad, matched SSH | Use `pgrep -af hermes` → `kill <PID>` |
| Gateway not starting after reboot | `loginctl enable-linger` not set | Run `loginctl enable-linger ubuntu` |

---

## 14. Warnings / Harmless Messages

These messages appear in logs but are **NOT errors** — you can safely ignore them:

| Message | What It Means | Action |
|---|---|---|
| `cua-driver warning: libXi.so.6 not found` | Optional desktop/display tool not present (server has no display) | **Ignore** — harmless |
| `Auxiliary Nous client unavailable` | Falls back to the primary model automatically | **Ignore** — bot still works |

> [!NOTE]
> Both of these are cosmetic warnings. The gateway and bot function normally when they appear.

---

## Quick Reference Card

### 🇬🇧 Full Setup Checklist

- [ ] Add 4 GB swap (1 GB server)
- [ ] `sudo apt install git curl screen libatomic1 fail2ban`
- [ ] `curl -fsSL https://install.hermes.sh | bash`
- [ ] `source ~/.bashrc`
- [ ] Create `~/.hermes/.env` with credentials
- [ ] `hermes config set model.provider nvidia`
- [ ] `hermes config set model.base_url https://integrate.api.nvidia.com/v1`
- [ ] `hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b`
- [ ] `hermes gateway install && hermes gateway start`
- [ ] `loginctl enable-linger ubuntu`
- [ ] Open Telegram → find bot → press START → send message ✅

---

*Last updated: 2026 | Tested on: Oracle Cloud Ubuntu 20.04 | AMD 1 vCPU Micro | 1 GB RAM + 4 GB Swap*
