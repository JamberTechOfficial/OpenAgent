# 03 — Hermes Agent Setup
# ہرمس ایجنٹ سیٹ اپ
# Hermes Agent Setup (Roman Urdu)

> **Status:** ✅ Tested on Oracle Cloud Ubuntu 20.04 | AMD 1 vCPU Micro | 1 GB RAM
> **Version Tested:** `hermes v0.22.5` with Python 3.14.9

---

## Table of Contents / فہرست / Fehrist

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

### 🇬🇧 English

**Hermes Agent** is an open-source AI agent made by **NousResearch**. It can be used via:
- **Telegram** (chat with it like a bot)
- **CLI** (command line interface)
- **API** (programmatic access)

It connects to **NVIDIA NIM API** (free tier available) to run powerful AI models without needing a local GPU.

- 🔗 GitHub: [https://github.com/NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)
- 🔗 Install script: `https://install.hermes.sh`

---

### 🇵🇰 اردو

**ہرمس ایجنٹ** ایک اوپن سورس اے آئی ایجنٹ ہے جو **NousResearch** نے بنایا ہے۔ اسے استعمال کیا جا سکتا ہے:
- **ٹیلیگرام** کے ذریعے (بوٹ کی طرح بات کریں)
- **CLI** کے ذریعے (کمانڈ لائن)
- **API** کے ذریعے (پروگرامنگ سے)

یہ **NVIDIA NIM API** (مفت ٹائر دستیاب) سے جڑتا ہے تاکہ بغیر مقامی GPU کے طاقتور AI ماڈلز چلا سکے۔

---

### 🗣️ Roman Urdu

**Hermes Agent** ek open-source AI agent hai jo **NousResearch** ne banaya hai. Ise use kiya ja sakta hai:
- **Telegram** ke zariye (bot ki tarah baat karein)
- **CLI** ke zariye (command line)
- **API** ke zariye (programming se)

Yeh **NVIDIA NIM API** (free tier available) se jurta hai taake bina local GPU ke powerful AI models chala sake.

---

## 2. Prerequisites

### 🇬🇧 English

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

### 🇵🇰 اردو

ہرمس انسٹال کرنے سے پہلے آپ کو یہ چیزیں **چاہیے**:

| ضرورت | کہاں سے لیں | گائیڈ |
|---|---|---|
| Ubuntu 20.04/22.04 سرور | Oracle Cloud (مفت) | `01-oracle-cloud-setup.md` |
| NVIDIA API کی | [build.nvidia.com](https://build.nvidia.com) | `02-nvidia-nim-api.md` |
| ٹیلیگرام بوٹ ٹوکن | ٹیلیگرام پر [@BotFather](https://t.me/BotFather) سے | نیچے دیکھیں |
| آپ کا ٹیلیگرام یوزر آئی ڈی | ٹیلیگرام پر [@userinfobot](https://t.me/userinfobot) سے | نیچے دیکھیں |

#### ٹیلیگرام بوٹ ٹوکن کیسے لیں
1. ٹیلیگرام کھولیں → `@BotFather` سرچ کریں
2. `/newbot` بھیجیں
3. ہدایات پر عمل کریں، بوٹ کا نام رکھیں
4. BotFather آپ کو ٹوکن دے گا جیسے: `1234567890:ABCdef...`  
   → یہی آپ کا `<your-bot-token>` ہے

#### ٹیلیگرام یوزر آئی ڈی کیسے لیں
1. ٹیلیگرام کھولیں → `@userinfobot` سرچ کریں
2. `/start` بھیجیں
3. یہ آپ کو نمبر والا آئی ڈی دے گا جیسے: `987654321`  
   → یہی آپ کا `<your-telegram-user-id>` ہے

---

### 🗣️ Roman Urdu

Hermes install karne se pehle aapko yeh cheezein **chahiye**:

| Zaroorat | Kahan Se Lein | Guide |
|---|---|---|
| Ubuntu 20.04/22.04 Server | Oracle Cloud (free) | `01-oracle-cloud-setup.md` |
| NVIDIA API Key | [build.nvidia.com](https://build.nvidia.com) | `02-nvidia-nim-api.md` |
| Telegram Bot Token | Telegram par @BotFather se | Neeche dekhein |
| Aapka Telegram User ID | Telegram par @userinfobot se | Neeche dekhein |

#### Telegram Bot Token kaise lein
1. Telegram kholein → `@BotFather` search karein
2. `/newbot` bhejein
3. Hidayaat par amal karein, bot ka naam rakhein
4. BotFather aapko token dega jaise: `1234567890:ABCdef...`  
   → Yahi aapka `<your-bot-token>` hai

#### Telegram User ID kaise lein
1. Telegram kholein → `@userinfobot` search karein
2. `/start` bhejein
3. Yeh aapko number wala ID dega jaise: `987654321`  
   → Yahi aapka `<your-telegram-user-id>` hai

---

## 3. ⚠️ CRITICAL: Add Swap BEFORE Installing (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

> [!CAUTION]
> **1 GB RAM** والے سرورز پر، ہرمس انسٹال کرنے سے پہلے آپ کو **لازمی طور پر** swap میموری شامل کرنی ہوگی۔ اس کے بغیر، سرور انسٹالیشن کے دوران **فریز ہو جائے گا**۔ یہ ٹیسٹنگ میں ثابت ہوا — سرور مکمل طور پر جام ہو گیا تھا۔

```bash
# مرحلہ 1: موجودہ swap چیک کریں (عام طور پر نئے سرور پر نہیں ہوتا)
free -h
swapon --show

# مرحلہ 2: 4 GB swap فائل بنائیں
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# مرحلہ 3: مستقل بنائیں (ریبوٹ کے بعد بھی رہے)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# مرحلہ 4: تصدیق کریں
free -h
# آپ کو "Swap:" کے نیچے ~4 GB نظر آنا چاہیے
```

---

### 🗣️ Roman Urdu

> [!CAUTION]
> **1 GB RAM** wale servers par, Hermes install karne se pehle aapko **lazmi tor par** swap memory shamil karni hogi. Iske bina, server installation ke dauran **freeze ho jayega**. Yeh testing mein sabit hua — server mukamal tor par jam gaya tha.

```bash
# Marhala 1: Maujuda swap check karein (aam tor par naye server par nahin hota)
free -h
swapon --show

# Marhala 2: 4 GB swap file banayein
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Marhala 3: Mustaqil banayein (reboot ke baad bhi rahe)
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Marhala 4: Tasdeeq karein
free -h
# Aapko "Swap:" ke neeche ~4 GB nazar aana chahiye
```

---

## 4. Install Prerequisites (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

پہلے ضروری سسٹم پیکیجز انسٹال کریں:

```bash
sudo apt-get update
sudo apt-get install -y git curl screen libatomic1 fail2ban
```

| پیکیج | کیوں ضروری ہے |
|---|---|
| `git` | عام ورژن کنٹرول |
| `curl` | ہرمس انسٹال اسکرپٹ ڈاؤنلوڈ کرتا ہے |
| `screen` | بیک گراؤنڈ سیشنز میں کمانڈ چلائیں |
| `libatomic1` | **لازمی** — بغیر اس کے `libatomic.so.1 not found` کی غلطی آتی ہے |
| `fail2ban` | سیکیورٹی: SSH بروٹ فورس حملوں کو خودکار روکتا ہے |

---

### 🗣️ Roman Urdu

Pehle zaroori system packages install karein:

```bash
sudo apt-get update
sudo apt-get install -y git curl screen libatomic1 fail2ban
```

| Package | Kyun Zaroori Hai |
|---|---|
| `git` | Aam version control |
| `curl` | Hermes install script download karta hai |
| `screen` | Background sessions mein command chalayein |
| `libatomic1` | **Lazmi** — bina iske `libatomic.so.1 not found` ki ghalti aati hai |
| `fail2ban` | Security: SSH brute force hamlon ko khudkar rokta hai |

---

## 5. Install Hermes (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

#### طریقہ 1 — براہ راست انسٹال

```bash
curl -fsSL https://install.hermes.sh | bash
```

#### طریقہ 2 — اسکرپٹ فائل کے ذریعے (اگر stdin مسائل ہوں)

اگر stdin/terminal سے متعلق غلطیاں آئیں تو یہ طریقہ استعمال کریں:

```bash
cat > /tmp/run_install.sh << 'EOF'
#!/bin/bash
curl -fsSL https://install.hermes.sh | bash
EOF
chmod +x /tmp/run_install.sh
/tmp/run_install.sh
```

#### انسٹالیشن کے بعد

```bash
# شیل پروفائل ریلوڈ کریں
source ~/.bashrc

# ہرمس انسٹال ہوا کہ نہیں چیک کریں
~/.local/bin/hermes --version
# متوقع: hermes v0.22.5
```

---

### 🗣️ Roman Urdu

#### Tareeqa 1 — Seedha Install

```bash
curl -fsSL https://install.hermes.sh | bash
```

#### Tareeqa 2 — Script File ke Zariye (Agar stdin masail hon)

Agar stdin/terminal se mutalliq ghaltiyan ayein to yeh tareeqa use karein:

```bash
cat > /tmp/run_install.sh << 'EOF'
#!/bin/bash
curl -fsSL https://install.hermes.sh | bash
EOF
chmod +x /tmp/run_install.sh
/tmp/run_install.sh
```

#### Installation ke Baad

```bash
# Shell profile reload karein
source ~/.bashrc

# Hermes install hua ke nahin check karein
~/.local/bin/hermes --version
# Matwaqqi: hermes v0.22.5
```

---

## 6. Configure Credentials (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

> [!IMPORTANT]
> نیچے دیے گئے placeholders کو اپنی **اصل** ویلیوز سے بدلیں۔ یہ فائل کبھی عام نہ کریں۔

```bash
# ہرمس کنفگ ڈائریکٹری بنائیں
mkdir -p ~/.hermes

# کریڈینشلز env فائل میں لکھیں
cat > ~/.hermes/.env << 'EOF'
NVIDIA_API_KEY=<your-nvidia-api-key>
TELEGRAM_BOT_TOKEN=<your-bot-token>
TELEGRAM_ALLOWED_USERS=<your-telegram-user-id>
EOF

# صرف آپ کا یوزر پڑھ سکے، اجازتیں محدود کریں
chmod 600 ~/.hermes/.env
```

| متغیر | کہاں ملے گا |
|---|---|
| `NVIDIA_API_KEY` | [build.nvidia.com](https://build.nvidia.com) سے |
| `TELEGRAM_BOT_TOKEN` | @BotFather سے |
| `TELEGRAM_ALLOWED_USERS` | @userinfobot سے (نمبری آئی ڈی) |

---

### 🗣️ Roman Urdu

> [!IMPORTANT]
> Neeche diye gaye placeholders ko apni **asal** values se badlein. Yeh file kabhi aam na karein.

```bash
# Hermes config directory banayein
mkdir -p ~/.hermes

# Credentials env file mein likhein
cat > ~/.hermes/.env << 'EOF'
NVIDIA_API_KEY=<your-nvidia-api-key>
TELEGRAM_BOT_TOKEN=<your-bot-token>
TELEGRAM_ALLOWED_USERS=<your-telegram-user-id>
EOF

# Sirf aapka user parh sake, ijazatein mahdood karein
chmod 600 ~/.hermes/.env
```

| Variable | Kahan Milega |
|---|---|
| `NVIDIA_API_KEY` | build.nvidia.com se |
| `TELEGRAM_BOT_TOKEN` | @BotFather se |
| `TELEGRAM_ALLOWED_USERS` | @userinfobot se (numberi ID) |

---

## 7. Configure Model (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

ہرمس کو NVIDIA NIM API استعمال کرنے اور ڈیفالٹ ماڈل سیٹ کرنے کی ہدایت دیں:

```bash
# AI پرووائیڈر NVIDIA پر سیٹ کریں
~/.local/bin/hermes config set model.provider nvidia

# NVIDIA NIM API بیس URL سیٹ کریں
~/.local/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1

# ڈیفالٹ ماڈل سیٹ کریں (بہترین تجربہ شدہ آپشن)
~/.local/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

---

### 🗣️ Roman Urdu

Hermes ko NVIDIA NIM API use karne aur default model set karne ki hidayat dein:

```bash
# AI provider NVIDIA par set karein
~/.local/bin/hermes config set model.provider nvidia

# NVIDIA NIM API base URL set karein
~/.local/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1

# Default model set karein (behtareen tajriba shuda option)
~/.local/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

---

## 8. NVIDIA Models That Work (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

درج ذیل ماڈلز کو **NVIDIA NIM مفت API** پر ٹیسٹ کیا گیا۔ نتائج آپ کے اکاؤنٹ ٹائر کے مطابق مختلف ہو سکتے ہیں۔

| ماڈل | رفتار | ٹول سپورٹ | حالت |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ~2 سیکنڈ | ✅ ہاں | ✅ **کام کرتا ہے — استعمال میں** |
| `minimaxai/minimax-m3.1-flash` | ~2 سیکنڈ | ✅ ہاں | ✅ کام کرتا ہے |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ~2 سیکنڈ | ✅ ہاں | ✅ کام کرتا ہے |
| `z-ai/glm-5.3` | ~55 سیکنڈ | ✅ ہاں | ✅ کام کرتا ہے (سست) |
| `nvidia/nemotron-3-super-120b-a12b` | — | — | ❌ 404 نہیں ملا |
| `moonshotai/kimi-k2.6` | — | — | ❌ 404 نہیں ملا |
| `deepseek-ai/deepseek-v4.1-flash` | — | — | ❌ ٹائم آؤٹ |

---

### 🗣️ Roman Urdu

Darj zail models ko **NVIDIA NIM free API** par test kiya gaya. Nataij aapke account tier ke mutabiq mukhtalif ho sakte hain.

| Model | Raftar | Tool Support | Halat |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ~2s | ✅ Haan | ✅ **Kaam karta hai — Istemal mein** |
| `minimaxai/minimax-m3.1-flash` | ~2s | ✅ Haan | ✅ Kaam karta hai |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ~2s | ✅ Haan | ✅ Kaam karta hai |
| `z-ai/glm-5.3` | ~55s | ✅ Haan | ✅ Kaam karta hai (sust) |
| `nvidia/nemotron-3-super-120b-a12b` | — | — | ❌ 404 nahin mila |
| `moonshotai/kimi-k2.6` | — | — | ❌ 404 nahin mila |
| `deepseek-ai/deepseek-v4.1-flash` | — | — | ❌ Timeout |

---

## 9. Install Telegram Gateway as System Service (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

ٹیلیگرام گیٹ وے ایک **یوزر لیول systemd سروس** کے طور پر چلتا ہے تاکہ بوٹ پر خودکار شروع ہو اور کریش پر ری اسٹارٹ ہو۔

```bash
# مرحلہ 1: گیٹ وے سروس انسٹال کریں
~/.local/bin/hermes gateway install

# مرحلہ 2: گیٹ وے شروع کریں
~/.local/bin/hermes gateway start

# مرحلہ 3: ریبوٹ پر خودکار شروع فعال کریں
loginctl enable-linger ubuntu

# مرحلہ 4: گیٹ وے حالت چیک کریں
~/.local/bin/hermes gateway status

# مرحلہ 5: لائیو لاگز دیکھیں (Ctrl+C سے روکیں)
journalctl --user -u hermes-gateway -f
```

**متوقع لاگ آؤٹ پٹ (صحت مند گیٹ وے):**
```
[Telegram] Connected to Telegram (polling mode)
[Gateway] Listening for messages...
```

---

### 🗣️ Roman Urdu

Telegram gateway ek **user-level systemd service** ke tor par chalta hai taake boot par khudkar shuru ho aur crash par restart ho.

```bash
# Marhala 1: Gateway service install karein
~/.local/bin/hermes gateway install

# Marhala 2: Gateway shuru karein
~/.local/bin/hermes gateway start

# Marhala 3: Reboot par khudkar shuru fail karein
loginctl enable-linger ubuntu

# Marhala 4: Gateway halat check karein
~/.local/bin/hermes gateway status

# Marhala 5: Live logs dekhein (Ctrl+C se rokein)
journalctl --user -u hermes-gateway -f
```

**Matwaqqi log output (sehatmand gateway):**
```
[Telegram] Connected to Telegram (polling mode)
[Gateway] Listening for messages...
```

---

## 10. Test the Bot

### 🇬🇧 English

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

### 🇵🇰 اردو

> [!IMPORTANT]
> بوٹ آپ کو **پہلے میسج نہیں** کر سکتا۔ آپ کو ہمیشہ بات شروع کرنی ہوگی۔

**ٹیسٹ کرنے کے مراحل:**
1. اپنے فون یا ڈیسک ٹاپ پر ٹیلیگرام کھولیں
2. اپنے بوٹ کا یوزرنیم سرچ کریں
3. **START** دبائیں (بہت ضروری — بغیر اس کے بوٹ آپ کو نہیں دیکھ سکتا)
4. کوئی بھی میسج لکھیں، مثلاً: `Hello! What can you do?`
5. چند سیکنڈ انتظار کریں — بوٹ جواب دے گا

**اگر بوٹ جواب نہ دے:**
```bash
journalctl --user -u hermes-gateway -n 50 --no-pager
```

---

### 🗣️ Roman Urdu

> [!IMPORTANT]
> Bot aapko **pehle message nahin** kar sakta. Aapko hamesha baat shuru karni hogi.

**Test karne ke marahil:**
1. Apne phone ya desktop par Telegram kholein
2. Apne bot ka username search karein
3. **START** dabayein (bohat zaroori — bina iske bot aapko nahin dekh sakta)
4. Koi bhi message likhein, masalan: `Hello! What can you do?`
5. Chand second intizar karein — bot jawab dega

**Agar bot jawab na de:**
```bash
journalctl --user -u hermes-gateway -n 50 --no-pager
```

---

## 11. Useful Commands (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

```bash
# ── گیٹ وے انتظام ──────────────────────────────────────────────

# گیٹ وے چل رہا ہے کہ نہیں چیک کریں
~/.local/bin/hermes gateway status

# گیٹ وے شروع کریں
~/.local/bin/hermes gateway start

# گیٹ وے دوبارہ شروع کریں (کنفگ تبدیلیاں لاگو کریں)
~/.local/bin/hermes gateway restart

# گیٹ وے بند کریں
~/.local/bin/hermes gateway stop

# ── لاگز ────────────────────────────────────────────────────────

# آخری 20 لاگ لائنیں دیکھیں
journalctl --user -u hermes-gateway -n 20 --no-pager

# لائیو لاگز فالو کریں
journalctl --user -u hermes-gateway -f

# ── سسٹم وسائل ───────────────────────────────────────────────────

# RAM اور swap استعمال چیک کریں
free -h

# ڈسک اسپیس چیک کریں
df -h

# لائیو پروسیس مانیٹر (q دبائیں بند کرنے کے لیے)
top
```

---

### 🗣️ Roman Urdu

```bash
# ── Gateway Intezam ─────────────────────────────────────────────

# Gateway chal raha hai ke nahin check karein
~/.local/bin/hermes gateway status

# Gateway shuru karein
~/.local/bin/hermes gateway start

# Gateway dobara shuru karein (config tabdeeliyan lagoo karein)
~/.local/bin/hermes gateway restart

# Gateway band karein
~/.local/bin/hermes gateway stop

# ── Logs ────────────────────────────────────────────────────────

# Aakhri 20 log lines dekhein
journalctl --user -u hermes-gateway -n 20 --no-pager

# Live logs follow karein
journalctl --user -u hermes-gateway -f

# ── System Wasail ─────────────────────────────────────────────────

# RAM aur swap istemal check karein
free -h

# Disk space check karein
df -h

# Live process monitor (q dabayein band karne ke liye)
top
```

---

## 12. Security Hardening (TESTED ✅)

### 🇬🇧 English

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

### 🇵🇰 اردو

> [!CAUTION]
> **یہ کرنے سے پہلے یقینی بنائیں کہ آپ کی SSH کی کام کر رہی ہے** ورنہ آپ سرور سے باہر ہو جائیں گے۔

#### SSH سیکیورٹی

```bash
# پاسورڈ لاگ ان، روٹ لاگ ان بند کریں؛ آتھ آزمائشیں محدود کریں
sudo bash -c 'cat > /etc/ssh/sshd_config.d/99-hardening.conf << EOF
PasswordAuthentication no
PermitRootLogin no
MaxAuthTries 3
EOF'

# نئی SSH کنفگ لاگو کریں
sudo systemctl restart ssh
```

#### Fail2ban کنفگریشن

```bash
# SSH تحفظ کے لیے fail2ban ترتیب دیں
sudo bash -c 'cat > /etc/fail2ban/jail.local << EOF
[sshd]
enabled = true
maxretry = 4
bantime = 3600
EOF'

# fail2ban ری اسٹارٹ کریں اور تصدیق کریں
sudo systemctl restart fail2ban
sudo fail2ban-client status sshd
```

> [!WARNING]
> **کبھی بھی `pkill -f hermes` نہ چلائیں** — اس pattern سے آپ کا SSH سیشن بھی بند ہو سکتا ہے۔ اس کے بجائے استعمال کریں:
> ```bash
> pgrep -af hermes   # پہلے PID تلاش کریں
> kill <PID>         # صرف وہ PID بند کریں
> ```

---

### 🗣️ Roman Urdu

> [!CAUTION]
> **Yeh karne se pehle yaqeeni banayein ke aapki SSH key kaam kar rahi hai** warna aap server se bahar ho jayenge.

#### SSH Security

```bash
# Password login, root login band karein; auth azmaishein mahdood karein
sudo bash -c 'cat > /etc/ssh/sshd_config.d/99-hardening.conf << EOF
PasswordAuthentication no
PermitRootLogin no
MaxAuthTries 3
EOF'

# Nayi SSH config lagoo karein
sudo systemctl restart ssh
```

#### Fail2ban Configuration

```bash
# SSH tahaffuz ke liye fail2ban tarteeb dein
sudo bash -c 'cat > /etc/fail2ban/jail.local << EOF
[sshd]
enabled = true
maxretry = 4
bantime = 3600
EOF'

# Fail2ban restart karein aur tasdeeq karein
sudo systemctl restart fail2ban
sudo fail2ban-client status sshd
```

> [!WARNING]
> **Kabhi bhi `pkill -f hermes` na chalayein** — is pattern se aapka SSH session bhi band ho sakta hai. Iske bajaye use karein:
> ```bash
> pgrep -af hermes   # Pehle PID talaash karein
> kill <PID>         # Sirf woh PID band karein
> ```

---

## 13. Common Errors & Fixes

### 🇬🇧 English

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

### 🇵🇰 اردو

| غلطی / علامت | وجہ | حل |
|---|---|---|
| انسٹال کے دوران سرور فریز ہوا | 1 GB RAM، کوئی swap نہیں | انسٹال سے **پہلے** 4 GB swap شامل کریں (سیکشن 3) |
| `libatomic.so.1 not found` | لائبریری غائب | `sudo apt install libatomic1` |
| `hermes: command not found` | PATH اپڈیٹ نہیں | `source ~/.bashrc` یا `~/.local/bin/hermes` استعمال کریں |
| `Gateway starting: deadline` | 1 GB سرور پر سست اسٹارٹ | نارمل — ٹیلیگرام سے ٹیسٹ کریں |
| بوٹ جواب نہیں دیتا | یوزر نے START نہیں دبایا | ٹیلیگرام میں بوٹ کھولیں → پہلے **START** دبائیں |
| ماڈل 404 غلطی | مفت ٹائر پر ماڈل دستیاب نہیں | `nvidia/nemotron-3-ultra-550b-a55b` پر سوئچ کریں |
| `pkill -f` نے SSH ڈسکنیکٹ کیا | pattern بہت وسیع تھا | `pgrep -af hermes` → `kill <PID>` استعمال کریں |
| ری بوٹ کے بعد گیٹ وے شروع نہیں | `loginctl enable-linger` سیٹ نہیں | `loginctl enable-linger ubuntu` چلائیں |

---

### 🗣️ Roman Urdu

| Ghalti / Alamat | Wajah | Hal |
|---|---|---|
| Install ke dauran server freeze hua | 1 GB RAM, koi swap nahin | Install se **pehle** 4 GB swap shamil karein (Section 3) |
| `libatomic.so.1 not found` | Library ghayab | `sudo apt install libatomic1` |
| `hermes: command not found` | PATH update nahin | `source ~/.bashrc` ya `~/.local/bin/hermes` use karein |
| `Gateway starting: deadline` | 1 GB server par sust start | Normal — Telegram se test karein |
| Bot jawab nahin deta | User ne START nahin dabaya | Telegram mein bot kholein → pehle **START** dabayein |
| Model 404 ghalti | Free tier par model dastiyab nahin | `nvidia/nemotron-3-ultra-550b-a55b` par switch karein |
| `pkill -f` ne SSH disconnect kiya | Pattern bohat wasee tha | `pgrep -af hermes` → `kill <PID>` use karein |
| Reboot ke baad gateway shuru nahin | `loginctl enable-linger` set nahin | `loginctl enable-linger ubuntu` chalayein |

---

## 14. Warnings / Harmless Messages

### 🇬🇧 English

These messages appear in logs but are **NOT errors** — you can safely ignore them:

| Message | What It Means | Action |
|---|---|---|
| `cua-driver warning: libXi.so.6 not found` | Optional desktop/display tool not present (server has no display) | **Ignore** — harmless |
| `Auxiliary Nous client unavailable` | Falls back to the primary model automatically | **Ignore** — bot still works |

> [!NOTE]
> Both of these are cosmetic warnings. The gateway and bot function normally when they appear.

---

### 🇵🇰 اردو

یہ پیغامات لاگز میں ظاہر ہوتے ہیں لیکن **غلطیاں نہیں ہیں** — آپ انہیں محفوظ طریقے سے نظر انداز کر سکتے ہیں:

| پیغام | کیا مطلب ہے | عمل |
|---|---|---|
| `cua-driver warning: libXi.so.6 not found` | اختیاری ڈیسک ٹاپ ٹول موجود نہیں (سرور پر ڈسپلے نہیں) | **نظر انداز کریں** |
| `Auxiliary Nous client unavailable` | خودکار بنیادی ماڈل پر واپس آ جاتا ہے | **نظر انداز کریں** — بوٹ کام کرتا رہتا ہے |

---

### 🗣️ Roman Urdu

Yeh paighamaat logs mein zahir hote hain lekin **ghaltiyan nahin hain** — aap inhen mehfooz tareeqe se nazar andaz kar sakte hain:

| Paigham | Kya Matlab Hai | Amal |
|---|---|---|
| `cua-driver warning: libXi.so.6 not found` | Ikhtiyari desktop tool maujood nahin (server par display nahin) | **Nazar andaz karein** |
| `Auxiliary Nous client unavailable` | Khudkar bunyadi model par wapas aa jata hai | **Nazar andaz karein** — bot kaam karta rehta hai |

---

## Quick Reference Card / فوری حوالہ / Foori Hawala

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

### 🇵🇰 مکمل سیٹ اپ چیک لسٹ

- [ ] 4 GB swap شامل کریں (1 GB سرور)
- [ ] ضروری پیکیجز انسٹال کریں
- [ ] ہرمس انسٹال اسکرپٹ چلائیں
- [ ] `source ~/.bashrc`
- [ ] کریڈینشلز کے ساتھ `~/.hermes/.env` بنائیں
- [ ] ماڈل کنفگریشن سیٹ کریں
- [ ] گیٹ وے انسٹال اور شروع کریں
- [ ] `loginctl enable-linger ubuntu`
- [ ] ٹیلیگرام → بوٹ → START → میسج ✅

### 🗣️ Mukammal Setup Check List

- [ ] 4 GB swap shamil karein (1 GB server)
- [ ] Zaroori packages install karein
- [ ] Hermes install script chalayein
- [ ] `source ~/.bashrc`
- [ ] Credentials ke saath `~/.hermes/.env` banayein
- [ ] Model configuration set karein
- [ ] Gateway install aur shuru karein
- [ ] `loginctl enable-linger ubuntu`
- [ ] Telegram → bot → START → message ✅

---

*Last updated: 2026 | Tested on: Oracle Cloud Ubuntu 20.04 | AMD 1 vCPU Micro | 1 GB RAM + 4 GB Swap*
*آخری اپ ڈیٹ: 2026 | ٹیسٹ: Oracle Cloud Ubuntu 20.04*
*Aakhri update: 2026 | Test: Oracle Cloud Ubuntu 20.04*
