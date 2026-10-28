# 🤖 AI Agents — Complete Setup Guide

> **By JT Community** | Created from real experience setting up AI agents on free cloud servers.
> 
> 📦 **Repo:** https://github.com/JamberTechOfficial/OpenAgent  
> 🌐 **Languages:** English

---

## 🗺️ Table of Contents

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

## 🚀 Quick Start

Not sure where to start? Answer these:

1. **Do you have a server?**
   - No → [Oracle Cloud Setup](docs/01-oracle-cloud-setup.md) (free forever) or [alternatives](docs/02-free-server-alternatives.md)
   - Yes → Continue to step 2

2. **Which AI agent do you want?**
   - Telegram bot assistant → [Hermes Agent](docs/03-hermes-agent-setup.md)
   - Something else → [Compare all agents](docs/04-other-ai-agents.md)

3. **Need a free AI API?**
   - → [NVIDIA API Guide](docs/05-nvidia-api-guide.md)

---

## ✅ What's Been Done (Real, Tested)

This guide is based on **real experience** — not theoretical. Here's what was actually done:

| Task | Status | Notes |
|---|---|---|
| Oracle Cloud account created | ✅ Done | AMD micro instance, Singapore region |
| Ubuntu 20.04 server deployed | ✅ Done | `ubuntu@<your-server-ip>` |
| 4 GB swap added | ✅ Done | CRITICAL — server freezes without it |
| Hermes v0.22.5 installed | ✅ Done | At `~/.local/bin/hermes` |
| NVIDIA API configured | ✅ Done | Using `nvidia/nemotron-3-ultra-550b-a55b` |
| Telegram gateway running | ✅ Done | As user systemd service |
| Security hardening | ✅ Done | SSH key-only, fail2ban |
| Reverse proxy setup | ❌ NOT DONE | Not needed (Telegram access only) |
| Cloudflare tunnel | ❌ NOT DONE | Not needed |

---

## ⚠️ Important Notes

- **No credentials in this repo** — all examples use `<placeholder>` values
- Everything marked ✅ was actually tested on a real Oracle Cloud server
- Things marked ❌ NOT DONE were deliberately skipped (not needed)
- The server only needs SSH (port 22) — no web server or public ports needed for Telegram bots

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

## 📞 Resources

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
