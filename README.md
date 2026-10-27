# 🤖 AI Agents — Complete Setup Guide | مکمل راہنما | Mukammal Rahnuma

> **By JT Community** | Created from real experience setting up AI agents on free cloud servers.
> 
> 📦 **Repo:** https://github.com/JamberTechOfficial/OpenAgent  
> 🌐 **Languages:** English | اردو | Roman Urdu

---

## 🗺️ Table of Contents | فہرست | Fehrist

| # | Guide | Description |
|---|---|---|
| 1 | [Oracle Cloud Setup](docs/01-oracle-cloud-setup.md) | Free VPS, credit cards, best regions |
| 2 | [Free Server Alternatives](docs/02-free-server-alternatives.md) | Render, Railway, GCP, AWS, Azure |
| 3 | [Hermes Agent Setup](docs/03-hermes-agent-setup.md) | ✅ Tested & working guide |
| 4 | [Other AI Agents](docs/04-other-ai-agents.md) | AutoGPT, CrewAI, AutoGen, MetaGPT... |
| 5 | [NVIDIA API Guide](docs/05-nvidia-api-guide.md) | Free API, phone verification issues |
| 6 | [Telegram Bot Setup](docs/06-telegram-bot-setup.md) | BotFather, User ID |
| 7 | [Troubleshooting](docs/07-troubleshooting.md) | All real errors & fixes |

---

## 🚀 Quick Start — کہاں سے شروع کریں — Kahan Se Shuru Karen?

### English
Not sure where to start? Answer these:

1. **Do you have a server?**
   - No → [Oracle Cloud Setup](docs/01-oracle-cloud-setup.md) (free forever) or [alternatives](docs/02-free-server-alternatives.md)
   - Yes → Continue to step 2

2. **Which AI agent do you want?**
   - Telegram bot assistant → [Hermes Agent](docs/03-hermes-agent-setup.md)
   - Something else → [Compare all agents](docs/04-other-ai-agents.md)

3. **Need a free AI API?**
   - → [NVIDIA API Guide](docs/05-nvidia-api-guide.md)

### اردو
یہ نہیں پتہ کہاں سے شروع کریں؟ یہ سوالات جواب دیں:

1. **کیا آپ کے پاس سرور ہے؟**
   - نہیں → [Oracle Cloud سیٹ اپ](docs/01-oracle-cloud-setup.md) (ہمیشہ کے لیے مفت) یا [متبادل آپشن](docs/02-free-server-alternatives.md)
   - ہاں → دوسرے سوال پر جائیں

2. **کون سا AI ایجنٹ چاہیے؟**
   - ٹیلیگرام بوٹ → [Hermes Agent](docs/03-hermes-agent-setup.md)
   - دوسرا → [سب کا موازنہ](docs/04-other-ai-agents.md)

### Roman Urdu
Pata nahi kahan se start karen? In sawalo ka jawab den:

1. **Kya apke pas server hai?**
   - Nahi → [Oracle Cloud Setup](docs/01-oracle-cloud-setup.md) (hamesha ke liye free) ya [alternatives](docs/02-free-server-alternatives.md)
   - Haan → agle sawal par jayen

2. **Konsa AI agent chahiye?**
   - Telegram bot → [Hermes Agent](docs/03-hermes-agent-setup.md)
   - Doosra → [Sab ka moazna](docs/04-other-ai-agents.md)

---

## ✅ What's Been Done (Real, Tested)

This guide is based on **real experience** — not theoretical. Here's what was actually done:

| Task | Status | Notes |
|---|---|---|
| Oracle Cloud account created | ✅ Done | AMD micro instance, chosen region |
| Ubuntu 20.04 server deployed | ✅ Done | Oracle Cloud AMD micro instance |
| 4 GB swap added | ✅ Done | CRITICAL — server freezes without it |
| Hermes v0.22.5 installed | ✅ Done | At `~/.local/bin/hermes` |
| NVIDIA API configured | ✅ Done | Using `nvidia/nemotron-3-ultra-550b-a55b` |
| Telegram gateway running | ✅ Done | As user systemd service |
| Security hardening | ✅ Done | SSH key-only, fail2ban |

---

## ⚠️ Important Notes | اہم نوٹ | Ahem Note

### English
- **No credentials in this repo** — all examples use `<placeholder>` values
- Everything marked ✅ was actually tested on a real Oracle Cloud server

### اردو
- **اس ریپو میں کوئی credentials نہیں** — سب مثالیں `<placeholder>` استعمال کرتی ہیں
- ✅ سے نشان زدہ سب کچھ اصل Oracle Cloud سرور پر ٹیسٹ ہوا
- ❌ والی چیزیں جان بوجھ کر چھوڑی گئیں (ضرورت نہیں تھی)

### Roman Urdu
- **Is repo mein koi credentials nahi** — sab examples `<placeholder>` use karte hain
- ✅ wali cheezain real Oracle Cloud server par tested hain
- ❌ wali cheezain deliberately skip ki gayin (zaroorat nahi thi)

---

## 🧑‍💻 About This Project

This repository documents the **real journey** of setting up an AI agent (Hermes) on a free Oracle Cloud server, accessible via Telegram.

**What we learned:**
- Oracle Cloud's free tier is genuinely free and the best option — if you can get past signup
- A 1 GB RAM server needs swap memory to survive package installation
- NVIDIA's free NIM API is excellent but phone verification blocks many countries
- Telegram + Hermes is a powerful and private setup

**Who is this for:**
- Pakistani / South Asian developers who want free AI tools
- Anyone who wants a personal AI assistant without recurring costs
- Developers learning about AI agents

---

## 📞 Resources | وسائل | Wasail

- Telegram BotFather: https://telegram.me/BotFather
- Get your Telegram User ID: https://telegram.me/userinfobot  
- NVIDIA NIM API: https://build.nvidia.com
- Oracle Cloud: https://cloud.oracle.com
- Hermes Agent: https://github.com/NousResearch/hermes-agent

---

## 🤝 Contributing

Found something wrong or want to add more guides? Open an issue or PR!

---

*Made with ❤️ by JT Community | Real experience, real solutions*

