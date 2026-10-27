# 02 — Free Server Alternatives for Hosting AI Agents / Bots
# مفت سرور متبادل — AI ایجنٹس / بوٹس کی ہوسٹنگ کے لیے
# Muft Server Alternatives — AI Agents / Bots Ki Hosting Ke Liye

---

## 1. Introduction

When **Oracle Cloud** doesn't work (card issues, regional capacity problems, etc.), there are several excellent free alternatives to host your AI agents and bots. This document covers every major option, their limits, and exactly how to deploy **Hermes** on them.

---

## ۱. تعارف

جب **Oracle Cloud** کام نہ کرے (کارڈ کا مسئلہ، ریجنل کیپیسٹی کی دشواری وغیرہ)، تو آپ کے AI ایجنٹس اور بوٹس کو ہوسٹ کرنے کے لیے کئی بہترین مفت متبادل موجود ہیں۔ یہ دستاویز ہر اہم آپشن، اس کی حدود، اور **Hermes** کو ان پر تعینات کرنے کا طریقہ بیان کرتی ہے۔

---

## 1. Taaruf (Introduction — Roman Urdu)

Jab **Oracle Cloud** kaam na kare (card ka masla, regional capacity ki dikkat, wagera), to aapke AI agents aur bots ko host karne ke liye kai behtareen muft mutabadil maujood hain. Yeh document har ahem option, uski hadood, aur **Hermes** ko un par deploy karne ka tareeqa bayan karta hai.

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

## ۲. موازنہ جدول

| پلیٹ فارم | مفت RAM | CPU | اسٹوریج | سلیپ؟ | کارڈ ضروری؟ | بہترین استعمال |
|---|---|---|---|---|---|---|
| **Oracle Cloud** | 24 GB (ARM) | 4 vCPU | 200 GB | ❌ نہیں | ✅ ہاں (چارج نہیں) | مجموعی طور پر بہترین مفت VPS |
| **Google Cloud** | 1 GB (e2-micro) | 0.25 vCPU | 30 GB | ❌ نہیں | ✅ ہاں | قابل بھروسہ، صرف US |
| **AWS Free Tier** | 1 GB (t3.micro) | 2 vCPU | 30 GB | ❌ نہیں | ✅ ہاں | صرف 12 ماہ |
| **Azure Free** | 1 GB (B1S) | 1 vCPU | 64 GB | ❌ نہیں | ✅ ہاں | صرف 12 ماہ |
| **Render** | 512 MB | مشترک | 1 GB | ⚠️ ہاں (15 منٹ) | ❌ نہیں | سادہ ویب ایپس |
| **Railway** | 512 MB | مشترک | 1 GB | ❌ نہیں (\$5 کریڈٹ) | ❌ نہیں | آسان ترین تعیناتی |
| **Fly.io** | 256 MB | مشترک | 3 GB | ⚠️ غیر سرگرمی کے بعد | ❌ نہیں | کنٹینرز |
| **Koyeb** | 512 MB | 0.1 vCPU | — | ❌ نہیں | ❌ نہیں | یورپی مفت ٹیئر |
| **Deta Space** | — | — | 10 GB | ❌ نہیں | ❌ نہیں | Python ایپس |

---

## 2. Muqabla Jadvaal (Comparison Table — Roman Urdu)

| Platform | Muft RAM | CPU | Storage | Sleep? | Card Zaroori? | Behtareen Istemal |
|---|---|---|---|---|---|---|
| **Oracle Cloud** | 24 GB (ARM) | 4 vCPU | 200 GB | ❌ Nahin | ✅ Haan (charge nahin) | Mujmooi taur par behtareen muft VPS |
| **Google Cloud** | 1 GB (e2-micro) | 0.25 vCPU | 30 GB | ❌ Nahin | ✅ Haan | Qaabil bharosa, sirf US |
| **AWS Free Tier** | 1 GB (t3.micro) | 2 vCPU | 30 GB | ❌ Nahin | ✅ Haan | Sirf 12 maah |
| **Azure Free** | 1 GB (B1S) | 1 vCPU | 64 GB | ❌ Nahin | ✅ Haan | Sirf 12 maah |
| **Render** | 512 MB | Mushtarak | 1 GB | ⚠️ Haan (15 min) | ❌ Nahin | Saadah web apps |
| **Railway** | 512 MB | Mushtarak | 1 GB | ❌ Nahin (\$5 credit) | ❌ Nahin | Aasaan tareen deployment |
| **Fly.io** | 256 MB | Mushtarak | 3 GB | ⚠️ Ghair-sargharmi ke baad | ❌ Nahin | Containers |
| **Koyeb** | 512 MB | 0.1 vCPU | — | ❌ Nahin | ❌ Nahin | European muft tier |
| **Deta Space** | — | — | 10 GB | ❌ Nahin | ❌ Nahin | Python apps |

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

## ۳. پلیٹ فارم تفصیلات

### 🏆 Oracle Cloud Always Free (بہترین)

- **2× AMD micro** VMs **یا** **4× Ampere A1 ARM** (24 GB RAM تک!)
- مکمل طور پر **مستقل** — کبھی ختم نہیں ہوتا
- مکمل **root access**، systemd، Docker — سب کچھ کام کرتا ہے
- 200 GB بلاک اسٹوریج شامل
- ⚠️ **مسئلہ:** سائن اپ مشکل — کارڈ کی تصدیق سخت ہے
- ✅ **حل:** بڑے بینک (میزان، HBL، UBL انٹرنیشنل) کا **فزیکل کریڈٹ کارڈ** استعمال کریں۔ پہلے انٹرنیشنل ٹرانزیکشن فعال کریں۔
- 🔗 https://cloud.oracle.com

---

### Google Cloud Free Tier

- **e2-micro** انسٹینس صرف **us-central1** یا **us-east1** میں — دیگر ریجنز پیسے لگتے ہیں!
- ہمیشہ مفت، **کبھی ختم نہیں**
- 1 مشترک vCPU، 1 GB RAM — Telegram بوٹ کے لیے کافی
- 30 GB اسٹینڈرڈ پرسسٹنٹ ڈسک
- کریڈٹ کارڈ چاہیے لیکن **مفت ٹیئر پر چارج نہیں ہوگا**
- 🔗 https://cloud.google.com

---

### AWS Free Tier

- **t2.micro** یا **t3.micro**: 1 GB RAM، 2 vCPU
- ⚠️ **صرف 12 ماہ** — پھر خود بخود چارجز شروع!
- **فوری طور پر بلنگ الرٹ سیٹ کریں!**
- 🔗 https://aws.amazon.com/free

---

### Azure Free

- **B1S**: 1 vCPU، 1 GB RAM
- ⚠️ **12 ماہ مفت** پھر چارجز
- 64 GB اسٹوریج
- 🔗 https://azure.microsoft.com/free

---

### Render (کارڈ نہیں چاہیے! ⚠️ سوتا ہے!)

- 512 MB RAM، مشترک CPU
- ⚠️ **15 منٹ غیر سرگرمی کے بعد سوجاتا ہے** — بوٹس کے لیے خراب
- **حل:** [UptimeRobot](https://uptimerobot.com) سے ہر 14 منٹ میں ping کریں
- 🔗 https://render.com

---

### Railway (آسان ترین! ⭐)

- **ہر ماہ \$5 مفت کریڈٹ** — کارڈ نہیں چاہیے
- 512 MB RAM — سوتا نہیں
- GitHub یا Docker سے تعیناتی
- 🔗 https://railway.app

---

### Fly.io

- **3 مفت VMs** (256 MB RAM فی VM)
- غیر سرگرمی کے بعد سوجاتا ہے مگر request آنے پر جاگتا ہے
- Docker کے ذریعے تعیناتی
- 🔗 https://fly.io

---

### Koyeb

- یورپی پلیٹ فارم (فرینکفرٹ، پیرس)
- 512 MB RAM، 0.1 vCPU مفت
- کارڈ نہیں چاہیے، سوتا نہیں
- 🔗 https://koyeb.com

---

## 3. Platform Tafseelaat (Roman Urdu)

### 🏆 Oracle Cloud Always Free (Behtareen)

- **2× AMD micro** VMs **ya** **4× Ampere A1 ARM** (24 GB RAM tak!)
- Mukammal taur par **mustaqil** — kabhi khatam nahin hota
- Mukammal **root access**, systemd, Docker — sab kuch kaam karta hai
- 200 GB block storage shamil
- ⚠️ **Masla:** Sign up mushkil — card ki tasdeeq sakht hai
- ✅ **Hal:** Bare bank (Meezan, HBL, UBL international) ka **physical credit card** istemaal karein. Pehle international transaction faal karein.
- 🔗 https://cloud.oracle.com

---

### Google Cloud Free Tier (Roman Urdu)

- **e2-micro** instance sirf **us-central1** ya **us-east1** mein — doosre regions mein paisa lagta hai!
- Hamesha muft, **kabhi khatam nahin**
- 1 mushtarak vCPU, 1 GB RAM — Telegram bot ke liye kaafi
- 30 GB persistent disk
- Credit card chahiye lekin **muft tier par charge nahin hoga**
- 🔗 https://cloud.google.com

---

### AWS Free Tier (Roman Urdu)

- **t2.micro** ya **t3.micro**: 1 GB RAM, 2 vCPU
- ⚠️ **Sirf 12 maah** — phir khud-ba-khud charges shuru!
- **Fori taur par billing alert set karein!**
- 🔗 https://aws.amazon.com/free

---

### Azure Free (Roman Urdu)

- **B1S**: 1 vCPU, 1 GB RAM
- ⚠️ **12 maah muft** phir charges
- 64 GB storage
- 🔗 https://azure.microsoft.com/free

---

### Render (Card nahin chahiye! ⚠️ Sota hai!)

- 512 MB RAM, mushtarak CPU
- ⚠️ **15 minute ghair-sargharmi ke baad so jata hai** — bots ke liye kharab
- **Hal:** [UptimeRobot](https://uptimerobot.com) se har 14 minute mein ping karein
- 🔗 https://render.com

---

### Railway (Aasaan tareen! ⭐ Roman Urdu)

- **Har maah \$5 muft credit** — card nahin chahiye
- 512 MB RAM — sota nahin
- GitHub ya Docker se deployment
- 🔗 https://railway.app

---

### Fly.io (Roman Urdu)

- **3 muft VMs** (256 MB RAM fi VM)
- Ghair-sargharmi ke baad sota hai magar request aane par jaagta hai
- Docker ke zariye deployment
- 🔗 https://fly.io

---

### Koyeb (Roman Urdu)

- European platform (Frankfurt, Paris)
- 512 MB RAM, 0.1 vCPU muft
- Card nahin chahiye, sota nahin
- 🔗 https://koyeb.com

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

## ۴. استعمال کے حساب سے سفارش

### Telegram بوٹ کے لیے (جیسے Hermes):

| ترجیح | پلیٹ فارم | کیوں |
|---|---|---|
| 🥇 **بہترین** | Oracle Cloud ARM A1 | 24 GB RAM، مستقل، root access |
| 🥈 **دوسرا بہترین** | Google Cloud e2-micro | 1 GB RAM، مستقل، صرف US |
| 🥉 **بغیر کارڈ** | Railway | ماہانہ \$5 کریڈٹ، نہیں سوتا |
| 🆓 **بغیر کارڈ، EU** | Koyeb | ہمیشہ آن، یورپی سرور |
| ⚠️ **گریز کریں** | Render | بوٹ سوتا ہے = پیغامات فوت |

---

## 4. Istemal Ke Hisaab Se Sifaarish (Roman Urdu)

### Telegram Bot Ke Liye (Jaise Hermes):

| Tarjeeh | Platform | Kyun |
|---|---|---|
| 🥇 **Behtareen** | Oracle Cloud ARM A1 | 24 GB RAM, mustaqil, root access |
| 🥈 **Doosra Behtareen** | Google Cloud e2-micro | 1 GB RAM, mustaqil, sirf US |
| 🥉 **Baghair Card** | Railway | Maahana \$5 credit, sota nahin |
| 🆓 **Baghair Card, EU** | Koyeb | Hamesha on, European server |
| ⚠️ **Gurez Karein** | Render | Bot sota hai = paighaamaat faut |

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

## ۵. Hermes ایجنٹ کو کتنے وسائل چاہئیں؟

| وسیلہ | کم از کم | سفارشی | مثالی |
|---|---|---|---|
| **RAM** | 1 GB + 2 GB swap | 2 GB | 4+ GB (Oracle A1!) |
| **CPU** | 1 vCPU | 2 vCPU | 4 vCPU |
| **ڈسک** | 5 GB | 10 GB | 20+ GB |
| **OS** | Ubuntu 20.04 | Ubuntu 22.04 LTS | Ubuntu 22.04 LTS |

### Swap کیسے شامل کریں (اگر RAM کم ہو):

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
free -h
```

---

## 5. Hermes Agent Ko Kitne Wasaail Chahiyein? (Roman Urdu)

| Wasila | Kam az Kam | Sifaarshi | Misaali |
|---|---|---|---|
| **RAM** | 1 GB + 2 GB swap | 2 GB | 4+ GB (Oracle A1!) |
| **CPU** | 1 vCPU | 2 vCPU | 4 vCPU |
| **Disk** | 5 GB | 10 GB | 20+ GB |
| **OS** | Ubuntu 20.04 | Ubuntu 22.04 LTS | Ubuntu 22.04 LTS |

### Swap Kaise Shamil Karein (Agar RAM Kam Ho):

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
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

## ۶. Render پر Hermes کو کیسے تعینات کریں

> ⚠️ **انتباہ:** Render کا مفت ٹیئر 15 منٹ غیر سرگرمی کے بعد سوجاتا ہے۔ اس دوران آپ کا بوٹ **Telegram پیغامات موصول نہیں کرسکے گا**۔ نیچے دی گئی UptimeRobot ترکیب استعمال کریں۔

**مرحلہ 1 — ریپو تیار کریں**
```
your-repo/
├── main.py
├── requirements.txt
├── .env          ← یہ GitHub پر مت ڈالیں!
```

**مرحلہ 2 — GitHub پر push کریں**
```bash
git init && git add . && git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/hermes-bot
git push -u origin main
```

**مرحلہ 3 — Render اکاؤنٹ بنائیں**
- https://render.com پر جائیں → سائن اپ کریں (کارڈ نہیں)
- **New +** → **Web Service** → GitHub جوڑیں → ریپو منتخب کریں

**مرحلہ 4 — سروس ترتیب دیں**
```
Build Command: pip install -r requirements.txt
Start Command: python main.py
Instance Type: Free
```

**مرحلہ 5 — ماحولیاتی متغیرات شامل کریں**
- **Environment** ٹیب → `BOT_TOKEN`، `OPENAI_API_KEY` وغیرہ شامل کریں

**مرحلہ 6 — تعیناتی کریں اور UptimeRobot سے جگائے رکھیں**
- https://uptimerobot.com پر جائیں → نیا مانیٹر → ہر 14 منٹ میں آپ کی Render URL کو ping

---

## 6. Render Par Hermes Ko Kaise Deploy Karein (Roman Urdu)

> ⚠️ **Intibah:** Render ka muft tier 15 minute ghair-sargharmi ke baad so jata hai. Is dauran aapka bot **Telegram paighaamaat nahi paayega**. Neeche di gayi UptimeRobot tarkeeb istemaal karein.

**Marhala 1 — Repo tayyar karein**
```
your-repo/
├── main.py
├── requirements.txt
├── .env          ← Yeh GitHub par mat daalna!
```

**Marhala 2 — GitHub par push karein**
```bash
git init && git add . && git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/hermes-bot
git push -u origin main
```

**Marhala 3 — Render account banayen**
- https://render.com par jayen → Sign up (card nahin)
- **New +** → **Web Service** → GitHub jorein → Repo chunein

**Marhala 4 — Service tarteeb dein**
```
Build Command: pip install -r requirements.txt
Start Command: python main.py
Instance Type: Free
```

**Marhala 5 — Environment variables shamil karein**
- `BOT_TOKEN`, `OPENAI_API_KEY` wagera daalein

**Marhala 6 — Deploy karein aur UptimeRobot se jagaye rakhein**
- https://uptimerobot.com → Naya monitor → Har 14 minute mein Render URL ko ping

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

## ۷. Google Cloud پر Hermes کو کیسے تعینات کریں

یہ **تجویز کردہ مفت متبادل** ہے — مستقل، 1 GB RAM، نہیں سوتا۔

**مرحلہ 1 — Google Cloud اکاؤنٹ بنائیں**
1. https://cloud.google.com پر جائیں
2. **Get started for free** پر کلک کریں
3. کارڈ درج کریں (مفت ٹیئر پر **چارج نہیں** ہوگا)
4. 90 دن کے لیے \$300 کریڈٹ + مستقل مفت ٹیئر

**مرحلہ 2 — Compute Engine فعال کریں**
- کنسول میں "Compute Engine" تلاش کریں → **Enable** کریں

**مرحلہ 3 — VM بنائیں**
```
Region: us-central1   ← لازمی یہی یا us-east1
Machine type: e2-micro ← یہی مفت ہے!
Boot disk: Ubuntu 22.04 LTS, 30 GB
```

**مرحلہ 4 — SSH سے جڑیں اور Hermes انسٹال کریں**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3 python3-pip python3-venv git -y
# Swap شامل کریں (1 GB RAM کے ساتھ ضروری ہے)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile && sudo mkswap /swapfile && sudo swapon /swapfile
```

**مرحلہ 5 — systemd سروس سے خودکار restart**
```bash
sudo systemctl enable hermes
sudo systemctl start hermes
sudo systemctl status hermes
```

---

## 7. Google Cloud Par Hermes Ko Kaise Deploy Karein (Roman Urdu)

Yeh **tajweez karda muft mutabadil** hai — mustaqil, 1 GB RAM, sota nahin.

**Marhala 1 — Google Cloud Account banayen**
1. https://cloud.google.com par jayen
2. **Get started for free** par click karein
3. Card darj karein (muft tier par **charge nahin** hoga)
4. 90 din ke liye \$300 credit + mustaqil muft tier

**Marhala 2 — Compute Engine faal karein**
- Console mein "Compute Engine" talash karein → **Enable** karein

**Marhala 3 — VM banayen**
```
Region: us-central1   ← Lazmi yahi ya us-east1
Machine type: e2-micro ← Yahi muft hai!
Boot disk: Ubuntu 22.04 LTS, 30 GB
```

**Marhala 4 — SSH se jorein aur Hermes install karein**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3 python3-pip python3-venv git -y
# Swap shamil karein (1 GB RAM ke saath zaroori)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile && sudo mkswap /swapfile && sudo swapon /swapfile

git clone https://github.com/yourusername/hermes-bot.git
cd hermes-bot
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

**Marhala 5 — systemd service se khudkar restart**
```bash
sudo systemctl enable hermes
sudo systemctl start hermes
sudo systemctl status hermes
```

✅ **Ho Gaya!** Hermes ab Google Cloud par 24/7 muft chal raha hai.

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
