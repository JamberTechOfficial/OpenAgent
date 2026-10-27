# 05 — NVIDIA NIM API Guide
# NVIDIA NIM API گائیڈ
# NVIDIA NIM API Guide (Roman Urdu)

> **🌐 Trilingual Guide | تین زبانوں میں گائیڈ | Teen Zubanon Mein Guide**
> English • اردو • Roman Urdu

---

## Table of Contents | فہرست مضامین | Fehrist

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

**🇬🇧 English**

NVIDIA NIM (NVIDIA Inference Microservices) API is a **free LLM API** provided by NVIDIA that gives you access to some of the most powerful AI language models in the world — including Nemotron, LLaMA, Mistral, and more.

- 🆓 **Free to use** — 1,000 API credits included with every new account
- 🤖 **Powerful models** — Nemotron Ultra, LLaMA 3.1, Mistral, MiniMax, and more
- 🔌 **OpenAI-compatible** — works with any client that supports the OpenAI API format
- 🌐 **Portal URL**: [https://build.nvidia.com](https://build.nvidia.com)
- ✅ **Works with**: Hermes Agent, LangChain, AutoGen, and other AI frameworks

---

**🇵🇰 اردو**

NVIDIA NIM API ایک **مفت LLM API** ہے جو NVIDIA نے فراہم کی ہے۔ اس کے ذریعے آپ دنیا کے سب سے طاقتور AI ماڈلز — جیسے Nemotron، LLaMA، Mistral — استعمال کر سکتے ہیں۔

- 🆓 **مفت استعمال** — ہر نئے اکاؤنٹ کے ساتھ 1,000 API کریڈٹس
- 🤖 **طاقتور ماڈلز** — Nemotron Ultra، LLaMA 3.1، Mistral، MiniMax وغیرہ
- 🔌 **OpenAI کے ساتھ ہم آہنگ** — کوئی بھی OpenAI-compatible کلائنٹ کام کرے گا
- 🌐 **ویب سائٹ**: [https://build.nvidia.com](https://build.nvidia.com)
- ✅ **یہ چیزوں کے ساتھ کام کرتا ہے**: Hermes Agent، LangChain، AutoGen

---

**🗣️ Roman Urdu**

NVIDIA NIM API aik **muft LLM API** hai jo NVIDIA ne provide ki hai. Iske zariye aap duniya ke sab se taqatwar AI models — jaise Nemotron, LLaMA, Mistral — use kar sakte hain.

- 🆓 **Muft use** — har naye account ke saath 1,000 API credits milte hain
- 🤖 **Taqatwar models** — Nemotron Ultra, LLaMA 3.1, Mistral, MiniMax wagera
- 🔌 **OpenAI ke saath compatible** — koi bhi OpenAI-compatible client kaam karega
- 🌐 **Website**: [https://build.nvidia.com](https://build.nvidia.com)
- ✅ **Yeh in cheezon ke saath kaam karta hai**: Hermes Agent, LangChain, AutoGen

---

## 2. How to Create an Account

**🇬🇧 English**

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

**🇵🇰 اردو**

1. [https://build.nvidia.com](https://build.nvidia.com) پر جائیں
2. اوپر دائیں طرف **"Sign In"** یا **"Get API Key"** پر کلک کریں
3. **NVIDIA Developer Account** بنائیں — اپنا ای میل اور پاس ورڈ درج کریں
4. **ای میل تصدیق کریں** — NVIDIA آپ کو تصدیقی لنک بھیجے گا
5. **فون نمبر کی تصدیق ضروری ہے:**
   - اپنا ملکی کوڈ اور فون نمبر درج کریں
   - آپ کو SMS کے ذریعے OTP ملے گا
   - OTP درج کریں
   - ⚠️ اگر آپ کا ملک فہرست میں نہیں یا SMS نہیں آتا → **نیچے سیکشن 4 دیکھیں**

---

**🗣️ Roman Urdu**

1. [https://build.nvidia.com](https://build.nvidia.com) par jayein
2. Upar dayen taraf **"Sign In"** ya **"Get API Key"** par click karein
3. **NVIDIA Developer Account** banayein — apna email aur password darj karein
4. **Email verify karein** — NVIDIA aapko verification link bhejega
5. **Phone number ki tasdeeq zaroori hai:**
   - Apna country code aur phone number darj karein
   - Aapko SMS ke zariye OTP milega
   - OTP darj karein
   - ⚠️ Agar aapka mulk list mein nahi ya SMS nahi aata → **neeche Section 4 dekhein**

---

## 3. Getting Your API Key

**🇬🇧 English**

1. After your account is created and phone is verified:
2. Go to [https://build.nvidia.com](https://build.nvidia.com) → click your **profile icon** or navigate to **"API Key"**
3. Click **"Generate API Key"**
4. Your key will be displayed — it starts with **`nvapi-`**
5. **⚠️ IMPORTANT: Copy and save it immediately!** You may not be shown this key again.

> [!CAUTION]
> Never share your API key publicly. Never commit it to GitHub. Store it securely in your `.env` file or a secrets manager. Use `<your-api-key>` as a placeholder in any shared configuration.

---

**🇵🇰 اردو**

1. اکاؤنٹ اور فون تصدیق کے بعد:
2. [https://build.nvidia.com](https://build.nvidia.com) پر جائیں → **پروفائل** یا **"API Key"** سیکشن پر جائیں
3. **"Generate API Key"** پر کلک کریں
4. آپ کی key ظاہر ہوگی — یہ **`nvapi-`** سے شروع ہوتی ہے
5. **⚠️ اہم: فوری طور پر copy کریں اور محفوظ کریں!** یہ دوبارہ نظر نہیں آ سکتی

> [!CAUTION]
> API key کو کبھی بھی عام نہ کریں۔ اسے GitHub پر commit نہ کریں۔ اسے `.env` فائل میں محفوظ رکھیں۔ مشترکہ کنفیگریشن میں `<your-api-key>` placeholder استعمال کریں۔

---

**🗣️ Roman Urdu**

1. Account aur phone verify hone ke baad:
2. [https://build.nvidia.com](https://build.nvidia.com) par jayein → **Profile** ya **"API Key"** section par jayein
3. **"Generate API Key"** par click karein
4. Aapki key dikhegi — yeh **`nvapi-`** se shuru hoti hai
5. **⚠️ Zaroori: Foran copy karein aur mehfooz karein!** Yeh dobara nazar nahi aa sakti

> [!CAUTION]
> API key kabhi bhi public mat karein. Ise GitHub par commit mat karein. Ise `.env` file mein mehfooz rakhein. Shared configuration mein `<your-api-key>` placeholder use karein.

---

## 4. Countries Where Phone Verification Has Issues

**🇬🇧 English**

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

**🇵🇰 اردو**

NVIDIA Developer Forums کی رپورٹس کی بنیاد پر، درج ذیل ممالک میں فون تصدیق کے مسائل دیکھے گئے ہیں:

### ❌ ڈراپ ڈاؤن سے غائب یا مسترد ممالک

| ملک | کوڈ | مسئلہ |
|---|---|---|
| 🇵🇰 **پاکستان** | +92 | عام طور پر ڈراپ ڈاؤن سے **مکمل طور پر غائب** |
| 🇨🇳 **چین** | +86 | SMS ڈیلیوری ناکام (carrier blocking) |
| 🇹🇷 **ترکی** | +90 | OTP ڈیلیوری میں مسائل |
| 🇧🇩 **بنگلہ دیش** | +880 | رپورٹ شدہ مسائل |
| 🇻🇳 **ویتنام** | +84 | رپورٹ شدہ مسائل |

### ⚠️ دیگر مسائل والے ممالک

- مختلف **افریقی ممالک** (نائیجیریا، گھانا وغیرہ)
- کچھ **مشرقی یورپی** ممالک
- **VoIP نمبرز** (کسی بھی ملک کے) — ہمیشہ مسترد
- **ورچوئل/ایپ نمبرز** (WhatsApp، Skype وغیرہ) — مسترد

### 🐛 عام بگ (درج ممالک کے لیے بھی)

- `"This phone number has reached its limit"` — **پہلی کوشش** پر بھی آتا ہے
- ڈراپ ڈاؤن **+1 (US) پر واپس چلا جاتا ہے** جب آپ کوئی اور ملک چنیں
- OTP **کبھی نہیں آتا** بار بار کوشش کے باوجود

---

**🗣️ Roman Urdu**

NVIDIA Developer Forums ki reports ke mutabiq, in mulkon mein phone verification ke masail note kiye gaye hain:

### ❌ Dropdown Se Ghayab Ya Radd Kiye Gaye Mulk

| Mulk | Code | Masla |
|---|---|---|
| 🇵🇰 **Pakistan** | +92 | Aksar dropdown mein **bilkul nazar nahi aata** |
| 🇨🇳 **China** | +86 | SMS delivery nakam (carrier blocking) |
| 🇹🇷 **Turkey** | +90 | OTP delivery mein masail |
| 🇧🇩 **Bangladesh** | +880 | Report shuda masail |
| 🇻🇳 **Vietnam** | +84 | Report shuda masail |

### ⚠️ Doosre Masla Vale Mulk

- Mukhtalif **Afriqi mulk** (Nigeria, Ghana wagera)
- Kuch **Mashriqi Yuropai** mulk
- **VoIP numbers** (kisi bhi mulk ke) — hamesha radd
- **Virtual/app numbers** (WhatsApp, Skype wagera) — radd

### 🐛 Aam Bugs (Registered Mulkon Ke Liye Bhi)

- `"This phone number has reached its limit"` — **pehli koshish** par bhi aata hai
- Dropdown **+1 (US) par wapas chala jata hai** jab aap doosra mulk chunein
- OTP **kabhi nahi aata** baar baar koshish ke bawajood

---

## 5. Solutions When Phone Verification Fails

**🇬🇧 English**

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

**🇵🇰 اردو**

### ✅ آپشن A: NVIDIA سپورٹ کو ای میل کریں (سرکاری — تجویز کردہ)

NVIDIA کی سرکاری سپورٹ کو ای میل کریں:

> **📧 ای میل:** `help@build.nvidia.com`
> **موضوع:** `Manual API Key Activation Request - Regional SMS Failure`

**ای میل میں شامل کریں:**
- آپ کا NVIDIA رجسٹرڈ ای میل
- آپ کا فون نمبر (ملکی کوڈ کے ساتھ، مثلاً +92 3xx xxxxxxx)
- خرابی کے اسکرین شاٹس
- وضاحت: *"میرے ملک کا SMS گیٹ وے آپ کے تصدیقی نظام میں شامل نہیں۔ برائے مہربانی میرا اکاؤنٹ دستی طور پر فعال کریں۔"*

---

### 🤝 آپشن B: کسی دوست کا فون نمبر استعمال کریں

- **امریکہ، برطانیہ، یا کینیڈا** میں رہنے والے دوست یا رشتہ دار سے مدد مانگیں
- وہ اپنے فون پر OTP وصول کریں
- آپ سے OTP شیئر کریں
- ✅ مکمل طور پر محفوظ اور جائز

---

### ⚠️ آپشن C: ورچوئل نمبر سروسز (خطرناک)

کچھ لوگ درج ذیل سروسز استعمال کرتے ہیں:
- **TextNow** (امریکی ورچوئل نمبرز)
- **Google Voice** (امریکی نمبر — ایکٹیویشن کے لیے اصل امریکی نمبر چاہیے)

> [!WARNING]
> یہ خطرناک ہے۔ NVIDIA ورچوئل نمبر کا پتہ لگا سکتا ہے اور اکاؤنٹ بند کر سکتا ہے۔ اپنی ذمہ داری پر استعمال کریں۔

---

### 🔄 آپشن D: متبادل APIs استعمال کریں

اگر NVIDIA کام نہ کرے، تو یہ بہترین مفت متبادل ہیں:

| سروس | لنک | فون چاہیے؟ | مفت کریڈٹ | نوٹ |
|---|---|---|---|---|
| **Groq** | [groq.com](https://groq.com) | ❌ نہیں | بڑا مفت ٹائر | تیز inference |
| **OpenRouter** | [openrouter.ai](https://openrouter.ai) | ❌ نہیں | کئی مفت ماڈلز | بہت زیادہ ماڈل |
| **Together AI** | [together.ai](https://together.ai) | ❌ نہیں | \$25 مفت کریڈٹ | اچھے ماڈل |
| **Google Gemini** | [aistudio.google.com](https://aistudio.google.com) | ❌ نہیں | مفت ٹائر | آسان signup |

---

**🗣️ Roman Urdu**

### ✅ Option A: NVIDIA Support Ko Email Karein (Sarkari — Tavsiyah Shuda)

NVIDIA ki sarkari support ko email karein:

> **📧 Email:** `help@build.nvidia.com`
> **Subject:** `Manual API Key Activation Request - Regional SMS Failure`

**Email mein shamil karein:**
- Aapka NVIDIA registered email
- Aapka phone number (country code ke saath, maslan +92 3xx xxxxxxx)
- Kharabi ke screenshots
- Wazahat: *"Mere mulk ka SMS gateway aapke system mein shamil nahi. Meherbani karke mera account dasti taur par fail karein."*

---

### 🤝 Option B: Kisi Dost Ka Phone Number Istemaal Karein

- **America, UK, ya Canada** mein rehne wale dost ya rishtedaar se madad mangein
- Woh apne phone par OTP receive karein
- Aapse OTP share karein
- ✅ Bilkul mehfooz aur jaiz

---

### ⚠️ Option C: Virtual Number Services (Khatarnak)

Kuch log in services istemaal karte hain:
- **TextNow** (Amriki virtual numbers)
- **Google Voice** (Amriki number — activation ke liye asal Amriki number chahiye)

> [!WARNING]
> Yeh khatarnak hai. NVIDIA virtual number pakad sakta hai aur account band kar sakta hai. Apni zimmedari par istemaal karein.

---

### 🔄 Option D: Mutabadil APIs Istemaal Karein

Agar NVIDIA kaam na kare, toh yeh behtareen muft mutabadil hain:

| Service | Link | Phone Chahiye? | Muft Credit | Note |
|---|---|---|---|---|
| **Groq** | [groq.com](https://groq.com) | ❌ Nahi | Bara muft tier | Tez inference |
| **OpenRouter** | [openrouter.ai](https://openrouter.ai) | ❌ Nahi | Kai muft models | Bohat models |
| **Together AI** | [together.ai](https://together.ai) | ❌ Nahi | \$25 muft credit | Aache models |
| **Google Gemini** | [aistudio.google.com](https://aistudio.google.com) | ❌ Nahi | Muft tier | Aasaan signup |

---

## 6. NVIDIA Models Available (Free Tier)

**🇬🇧 English**

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

**🇵🇰 اردو**

درج ذیل ماڈلز **مفت ٹائر اکاؤنٹ پر ٹیسٹ کر کے تصدیق کیے گئے** ہیں۔ ماڈل کی دستیابی مختلف اکاؤنٹس میں فرق ہو سکتی ہے۔

### ✅ کام کرنے والے ماڈلز

| ماڈل کا نام | Hermes میں استعمال | رفتار | نوٹس |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ✅ **تجویز کردہ** | ~2s | بہترین معیار |
| `minimaxai/minimax-m3.1-flash` | ✅ اچھا بیک اپ | ~2s | تیز اور قابل اعتماد |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ✅ کام کرتا ہے | ~2s | ہلکا، پھر بھی اچھا |
| `z-ai/glm-5.3` | ✅ کام کرتا ہے | ~55s | ⚠️ بہت سست |
| `meta/llama-3.1-8b-instruct` | دستیابی چیک کریں | ~1s | ہلکا پھلکا |
| `mistralai/mistral-7b-instruct` | دستیابی چیک کریں | ~1s | ہلکا پھلکا |

### ❌ غلطی دینے والے ماڈلز (ٹیسٹ کیے گئے اکاؤنٹ پر)

| ماڈل کا نام | غلطی |
|---|---|
| `nvidia/nemotron-3-super-120b-a12b` | 404 Not Found |
| `nvidia/llama-3.1-nemotron-ultra-253b-v1` | 404 Not Found |
| `deepseek-ai/deepseek-v4.1-flash` | Timeout |

> [!NOTE]
> ماڈل کی دستیابی اکاؤنٹ اور علاقے کے مطابق مختلف ہو سکتی ہے۔ مفت 1,000 کریڈٹس ختم ہونے کے بعد ادائیگی یا مفت متبادل API استعمال کرنا پڑے گا۔

---

**🗣️ Roman Urdu**

Yeh models **muft tier account par test karke tasdeek kiye gaye** hain. Model ki dastiyabi mukhtalif accounts mein farq ho sakti hai.

### ✅ Kaam Karne Wale Models

| Model Ka Naam | Hermes Mein Istemaal | Raftar | Notes |
|---|---|---|---|
| `nvidia/nemotron-3-ultra-550b-a55b` | ✅ **Tavsiyah Shuda** | ~2s | Behtareen mayaar |
| `minimaxai/minimax-m3.1-flash` | ✅ Acha backup | ~2s | Tez aur qabil-e-itmad |
| `nvidia/nemotron-3.5-lightning-30b-a3b` | ✅ Kaam karta hai | ~2s | Halka, phir bhi acha |
| `z-ai/glm-5.3` | ✅ Kaam karta hai | ~55s | ⚠️ Bohat sust |
| `meta/llama-3.1-8b-instruct` | Dastiyabi check karein | ~1s | Halka phulka |
| `mistralai/mistral-7b-instruct` | Dastiyabi check karein | ~1s | Halka phulka |

### ❌ Ghalti Dene Wale Models (Test Kiye Gaye Account Par)

| Model Ka Naam | Ghalti |
|---|---|
| `nvidia/nemotron-3-super-120b-a12b` | 404 Not Found |
| `nvidia/llama-3.1-nemotron-ultra-253b-v1` | 404 Not Found |
| `deepseek-ai/deepseek-v4.1-flash` | Timeout |

> [!NOTE]
> Model ki dastiyabi account aur علاقے ke mutabiq mukhtalif ho sakti hai. Muft 1,000 credits khatam hone ke baad payment ya muft mutabadil API istemaal karna parega.

---

## 7. Using NVIDIA API with Hermes

**🇬🇧 English**

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

**🇵🇰 اردو**

API key ملنے کے بعد، Hermes کو NVIDIA استعمال کرنے کے لیے configure کریں:

### مرحلہ 1 — Provider کنفیگریشن سیٹ کریں

```bash
# NVIDIA کو provider سیٹ کریں
~/.local/bin/hermes config set model.provider nvidia

# NVIDIA NIM API کا base URL سیٹ کریں
~/.local/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1

# اپنا پسندیدہ ڈیفالٹ ماڈل سیٹ کریں
~/.local/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

### مرحلہ 2 — `.env` فائل میں API Key سیٹ کریں

اپنی Hermes `.env` فائل کھولیں اور یہ شامل کریں:

```bash
# NVIDIA NIM API Key
NVIDIA_API_KEY=<your-api-key>
```

> [!IMPORTANT]
> `<your-api-key>` کی جگہ اپنی اصل key لکھیں جو `nvapi-` سے شروع ہوتی ہے۔ اصل key کو کبھی ایسی config فائلوں میں نہ ڈالیں جو version control میں ہوں۔

---

**🗣️ Roman Urdu**

API key milne ke baad, Hermes ko NVIDIA istemaal karne ke liye configure karein:

### Marhala 1 — Provider Configuration Set Karein

```bash
# NVIDIA ko provider set karein
~/.local/bin/hermes config set model.provider nvidia

# NVIDIA NIM API ka base URL set karein
~/.local/bin/hermes config set model.base_url https://integrate.api.nvidia.com/v1

# Apna pasandida default model set karein
~/.local/bin/hermes config set model.default nvidia/nemotron-3-ultra-550b-a55b
```

### Marhala 2 — `.env` File Mein API Key Set Karein

Apni Hermes `.env` file kholein aur yeh shamil karein:

```bash
# NVIDIA NIM API Key
NVIDIA_API_KEY=<your-api-key>
```

> [!IMPORTANT]
> `<your-api-key>` ki jagah apni asal key likhein jo `nvapi-` se shuru hoti hai. Asal key ko kabhi aisi config files mein mat dalein jo version control mein hon.

---

## 8. Test Your API Key

**🇬🇧 English**

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

**🇵🇰 اردو**

اپنی API key کو test کرنے کے لیے درج ذیل `curl` کمانڈ استعمال کریں:

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

### ✅ کامیاب جواب کی مثال

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

### ❌ عام غلطیاں

| ایرر کوڈ | مطلب | حل |
|---|---|---|
| `401 Unauthorized` | غلط API key | اپنی key دوبارہ چیک کریں — `nvapi-` سے شروع ہونی چاہیے |
| `404 Not Found` | ماڈل دستیاب نہیں | سیکشن 6 سے کوئی اور ماڈل آزمائیں |
| `429 Too Many Requests` | حد سے زیادہ درخواستیں | انتظار کریں، یا باقی کریڈٹس چیک کریں |
| `408 Timeout` | ماڈل بہت سست | تیز ماڈل پر سوئچ کریں |

---

**🗣️ Roman Urdu**

Apni API key ko test karne ke liye yeh `curl` command istemaal karein:

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

### ✅ Kamiyab Jawab Ki Misal

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

### ❌ Aam Ghaltiyan

| Error Code | Matlab | Hal |
|---|---|---|
| `401 Unauthorized` | Ghalat API key | Apni key dobara check karein — `nvapi-` se shuru honi chahiye |
| `404 Not Found` | Model dastiyab nahi | Section 6 se koi aur model azmaein |
| `429 Too Many Requests` | Ziada requests | Intezaar karein, ya baqi credits check karein |
| `408 Timeout` | Model bohat sust | Tez model par switch karein |

---

## Quick Reference | فوری حوالہ | Fori Hawala

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
