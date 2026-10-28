# 05 — NVIDIA NIM API Guide

---

## Table of Contents

1. [What is NVIDIA NIM API?](#1-what-is-nvidia-nim-api)
2. [How to Create an Account](#2-how-to-create-an-account)
3. [Getting Your API Key](#3-getting-your-api-key)
4. [Countries Where Phone Verification Has Issues](#4-countries-where-phone-verification-has-issues)
5. [Solutions When Phone Verification Fails](#5-solutions-when-phone-verification-fails)
6. [NVIDIA Models Available (Free Tier)](#6-nvidia-models-available-free-tier)
7. [Using NVIDIA API with Hermes](#7-using-nvidia-api-with-hermes)
8. [Test Your API Key](#8-test-your-api-key)

---

## 1. What is NVIDIA NIM API?

NVIDIA NIM (NVIDIA Inference Microservices) API is a **free LLM API** provided by NVIDIA that gives you access to some of the most powerful AI language models in the world — including Nemotron, LLaMA, Mistral, and more.

- 🆓 **Free to use** — 1,000 API credits included with every new account
- 🤖 **Powerful models** — Nemotron Ultra, LLaMA 3.1, Mistral, MiniMax, and more
- 🔌 **OpenAI-compatible** — works with any client that supports the OpenAI API format
- 🌐 **Portal URL**: [https://build.nvidia.com](https://build.nvidia.com)
- ✅ **Works with**: Hermes Agent, LangChain, AutoGen, and other AI frameworks

---

## 2. How to Create an Account

1. Go to [https://build.nvidia.com](https://build.nvidia.com)
2. Click **"Sign In"** or **"Get API Key"** in the top right corner
3. Create a **NVIDIA Developer Account** — provide your email address and set a password
4. **Verify your email** — NVIDIA will send a verification link to your inbox
5. **Phone number verification is required:**
   - Enter your country code and phone number
   - You will receive an SMS with a One-Time Password (OTP)
   - Enter the OTP to complete verification
   - ⚠️ If your country is not listed or SMS doesn't arrive → **see Section 4 below**

---

## 3. Getting Your API Key

1. After your account is created and phone is verified:
2. Go to [https://build.nvidia.com](https://build.nvidia.com) → click your **profile icon** or navigate to **"API Key"**
3. Click **"Generate API Key"**
4. Your key will be displayed — it starts with **`nvapi-`**
5. **⚠️ IMPORTANT: Copy and save it immediately!** You may not be shown this key again.

> [!CAUTION]
> Never share your API key publicly. Never commit it to GitHub. Store it securely in your `.env` file or a secrets manager. Use `<your-api-key>` as a placeholder in any shared configuration.

---

## 4. Countries Where Phone Verification Has Issues

Based on community reports from NVIDIA Developer Forums, the following countries have experienced phone verification problems:

### ❌ Confirmed Missing from Dropdown or Rejected

| Country | Code | Issue |
|---|---|---|
| 🇵🇰 **Pakistan** | +92 | Frequently reported **MISSING** from dropdown entirely |
| 🇨🇳 **China** | +86 | SMS delivery failures (carrier blocking) |
| 🇹🇷 **Turkey** | +90 | Reported issues with OTP delivery |
| 🇧🇩 **Bangladesh** | +880 | Reported issues |
| 🇻🇳 **Vietnam** | +84 | Reported issues |

### ⚠️ Also Reported Problematic

- Various **African countries** (Nigeria, Ghana, etc.)
- Some **Eastern European** countries
- **VoIP numbers** (any country) — always rejected
- **Virtual/app numbers** (WhatsApp numbers, Skype, etc.) — rejected

### 🐛 Common Bugs Even for Listed Countries

- `"This phone number has reached its limit"` — bug that appears even on the **first attempt**
- Dropdown **resets back to +1 (US)** when you try to select a different country
- OTP **never arrives** even after multiple retries

---

## 5. Solutions When Phone Verification Fails

### ✅ Option A: Email NVIDIA Support (Official — Recommended)

Send an email to NVIDIA's official support:

> **📧 Email:** `help@build.nvidia.com`
> **Subject:** `Manual API Key Activation Request - Regional SMS Failure`

**Include in your email:**
- Your registered NVIDIA email address
- Your phone number (with country code, e.g. +92 3xx xxxxxxx)
- Screenshots of the error you are seeing
- Explanation: *"My country's SMS gateway is not supported by your verification system. Kindly activate my account manually."*

---

### 🤝 Option B: Use a Friend's Phone Number

- Ask a friend or family member who lives in the **US, UK, or Canada**
- They receive the OTP on their phone
- They share the OTP with you
- ✅ Completely safe and officially allowed

---

### ⚠️ Option C: Virtual Number Services (Risky)

Some community members have used services such as:
- **TextNow** (US virtual numbers)
- **Google Voice** (US numbers — requires existing US number to activate)

> [!WARNING]
> This approach carries risk. NVIDIA may detect virtual numbers and suspend or ban your account. Use at your own risk.

---

### 🔄 Option D: Use Alternative APIs

If NVIDIA still doesn't work for you, here are excellent free alternatives:

| Service | URL | Phone Needed? | Free Credits | Notes |
|---|---|---|---|---|
| **Groq** | [groq.com](https://groq.com) | ❌ No | Generous free tier | Fast inference |
| **OpenRouter** | [openrouter.ai](https://openrouter.ai) | ❌ No | Many free models | Huge model variety |
| **Together AI** | [together.ai](https://together.ai) | ❌ No | \$25 free credit | Good models |
| **Google Gemini** | [aistudio.google.com](https://aistudio.google.com) | ❌ No | Free tier | Easy signup |

---

## 6. NVIDIA Models Available (Free Tier)

The following models were **tested and confirmed working** on a free-tier account. Model availability can vary between accounts.

### ✅ Working Models

| Model Name | Use In Hermes | Speed | Notes |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ✅ **Recommended** | ~2s | Best quality output |
| `minimaxai/minimax-m3.1-flash` | ✅ Good backup | ~2s | Fast & reliable |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ✅ Works | ~2s | Lighter, still good |
| `z-ai/glm-5.3` | ✅ Works | ~55s | ⚠️ Very SLOW |
| `meta/llama-3.1-8b-instruct` | Check availability | ~1s | Lightweight |
| `mistralai/mistral-7b-instruct` | Check availability | ~1s | Lightweight |

### ❌ Models That Gave Errors (on Tested Account)

| Model Name | Error |
|---|---|
| `nvidia/nemotron-3-super-120b-a12b` | 404 Not Found |
| `nvidia/llama-3.1-nemotron-ultra-253b-v1` | 404 Not Found |
| `deepseek-ai/deepseek-v4.1-flash` | Timeout |

> [!NOTE]
> Model availability varies by account and region. The free 1,000 credits may expire; after that you will need to add a payment method or switch to a free alternative API.

---

## 7. Using NVIDIA API with Hermes

Once you have your API key, configure Hermes to use NVIDIA as the model provider:

### Step 1 — Set Provider Configuration

```bash
# Set NVIDIA as the provider
~/.local/bin/hermes config set model.provider nvidia

# Set the NVIDIA NIM API base URL
~/.local/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1

# Set your preferred default model
~/.local/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

### Step 2 — Set API Key in `.env` File

Open your Hermes `.env` file and add:

```bash
# NVIDIA NIM API Key
NVIDIA_API_KEY=<your-api-key>
```

> [!IMPORTANT]
> Replace `<your-api-key>` with your actual key starting with `nvapi-`. Never hardcode the real key in config files that are committed to version control.

---

## 8. Test Your API Key

Use the following `curl` command to verify your API key is working correctly:

```bash
curl https://integrate.api.nvidia.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <your-api-key>" \
  -d '{
    "model": "nvidia/nemotron-3-ultra-550b-a55b",
    "messages": [{"role": "user", "content": "Say hello"}],
    "max_tokens": 50
  }'
```

### ✅ Expected Successful Response

```json
{
  "id": "chatcmpl-...",
  "object": "chat.completion",
  "choices": [
    {
      "message": {
        "role": "assistant",
        "content": "Hello! How can I help you today?"
      }
    }
  ]
}
```

### ❌ Common Error Responses

| Error Code | Meaning | Fix |
|---|---|---|
| `401 Unauthorized` | Invalid API key | Double-check your key — must start with `nvapi-` |
| `404 Not Found` | Model not available | Try a different model from Section 6 |
| `429 Too Many Requests` | Rate limit hit | Wait and retry, or check remaining credits |
| `408 Timeout` | Model too slow | Switch to a faster model |

---

## Quick Reference

| Item | Value |
|---|---|
| **NVIDIA Build Portal** | https://build.nvidia.com |
| **API Base URL** | https://integrate.api.nvidia.com/v1 |
| **API Key Format** | `nvapi-xxxxxxxxxxxx` |
| **Free Credits** | 1,000 per account |
| **Support Email** | help@build.nvidia.com |
| **Recommended Model** | `nvidia/nemotron-3-ultra-550b-a55b` |
| **Pakistan Phone (+92)** | ⚠️ May be missing from dropdown — email support |

---

*Last updated: 2026 | JT Community Hermes Project*
