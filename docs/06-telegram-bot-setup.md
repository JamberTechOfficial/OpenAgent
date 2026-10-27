# 06 — Telegram Bot Setup
# ٹیلیگرام بوٹ سیٹ اپ
# Telegram Bot Setup (Roman Urdu)

---

## 1. What You Need
## آپ کو کیا چاہیے
## Aap Ko Kya Chahiye

**English:**
- A Telegram account
- A server (see other guides)

**اردو:**
- ایک ٹیلیگرام اکاؤنٹ
- ایک سرور (دوسری گائیڈز دیکھیں)

**Roman Urdu:**
- Ek Telegram account
- Ek server (dosri guides dekhein)

---

## 2. Create a Telegram Bot via @BotFather
## @BotFather کے ذریعے ٹیلیگرام بوٹ بنائیں
## @BotFather Ke Zariye Telegram Bot Banayein

**English:**

1. Open Telegram
2. Search for: **@BotFather** → https://telegram.me/BotFather
3. Press START
4. Send: `/newbot`
5. Enter bot name: (e.g., "My Hermes Bot")
6. Enter bot username: (must end in `bot`, e.g., `myhermesbot` or `my_hermes_bot`)
7. BotFather replies with your **Bot Token** — looks like: `1234567890:AAFxxxxx...`
8. SAVE this token — you'll need it

**اردو:**

1. ٹیلیگرام کھولیں
2. تلاش کریں: **@BotFather** → https://telegram.me/BotFather
3. START دبائیں
4. بھیجیں: `/newbot`
5. بوٹ کا نام درج کریں: (مثلاً، "My Hermes Bot")
6. بوٹ کا یوزرنیم درج کریں: (آخر میں `bot` ہونا ضروری ہے، مثلاً `myhermesbot` یا `my_hermes_bot`)
7. BotFather آپ کو **Bot Token** دے گا — یہ اس طرح نظر آتا ہے: `1234567890:AAFxxxxx...`
8. یہ ٹوکن محفوظ کریں — آپ کو اس کی ضرورت ہوگی

**Roman Urdu:**

1. Telegram kholein
2. Talash karein: **@BotFather** → https://telegram.me/BotFather
3. START dabaein
4. Bhejein: `/newbot`
5. Bot ka naam darj karein: (maslan, "My Hermes Bot")
6. Bot ka username darj karein: (aakhir mein `bot` hona zaroori hai, maslan `myhermesbot` ya `my_hermes_bot`)
7. BotFather aap ko **Bot Token** dega — yeh is tarah nazar aata hai: `1234567890:AAFxxxxx...`
8. Yeh token mahfooz karein — aap ko iski zaroorat hogi

---

## 3. Get Your Telegram User ID
## اپنا ٹیلیگرام یوزر ID حاصل کریں
## Apna Telegram User ID Hasil Karein

**English:**

1. Open Telegram
2. Search for: **@userinfobot** → https://telegram.me/userinfobot
3. Press START
4. It replies with your user info including your **numeric User ID** (e.g., <your-user-id>)
5. SAVE this ID

**اردو:**

1. ٹیلیگرام کھولیں
2. تلاش کریں: **@userinfobot** → https://telegram.me/userinfobot
3. START دبائیں
4. یہ آپ کی یوزر معلومات کے ساتھ جواب دے گا جس میں آپ کا **عددی یوزر ID** شامل ہے (مثلاً، <your-user-id>)
5. یہ ID محفوظ کریں

**Roman Urdu:**

1. Telegram kholein
2. Talash karein: **@userinfobot** → https://telegram.me/userinfobot
3. START dabaein
4. Yeh aap ki user malumat ke saath jawab dega jis mein aap ka **numeric User ID** shamil hai (maslan, <your-user-id>)
5. Yeh ID mahfooz karein

---

## 4. Add to Hermes .env
## Hermes .env میں شامل کریں
## Hermes .env Mein Shamil Karein

**English:**

```bash
TELEGRAM_BOT_TOKEN=<your-bot-token-from-botfather>
TELEGRAM_ALLOWED_USERS=<your-numeric-user-id>
```

**اردو:**

اپنی `.env` فائل میں یہ لائنیں شامل کریں:

```bash
TELEGRAM_BOT_TOKEN=<your-bot-token-from-botfather>
TELEGRAM_ALLOWED_USERS=<your-numeric-user-id>
```

**Roman Urdu:**

Apni `.env` file mein yeh lines shamil karein:

```bash
TELEGRAM_BOT_TOKEN=<your-bot-token-from-botfather>
TELEGRAM_ALLOWED_USERS=<your-numeric-user-id>
```

---

## 5. Test the Bot
## بوٹ کو ٹیسٹ کریں
## Bot Ko Test Karein

**English:**

1. The bot CANNOT message you first — you must initiate
2. Find your bot in Telegram (search @yourbotusername)
3. Press START
4. Send any message
5. If Hermes gateway is running, you'll get a reply!

**اردو:**

1. بوٹ آپ کو پہلے میسج نہیں کر سکتا — آپ کو شروع کرنا ہوگا
2. ٹیلیگرام میں اپنا بوٹ تلاش کریں (@yourbotusername تلاش کریں)
3. START دبائیں
4. کوئی بھی پیغام بھیجیں
5. اگر Hermes gateway چل رہا ہے، آپ کو جواب ملے گا!

**Roman Urdu:**

1. Bot aap ko pehle message nahi kar sakta — aap ko shuru karna hoga
2. Telegram mein apna bot talash karein (@yourbotusername talash karein)
3. START dabaein
4. Koi bhi paigham bhejein
5. Agar Hermes gateway chal raha hai, aap ko jawab milega!

---

## 6. Multiple Allowed Users
## متعدد اجازت یافتہ صارفین
## Mutaddid Ijazat Yafta Sarifeen

**English:**

To allow multiple users:
```bash
TELEGRAM_ALLOWED_USERS=123456789,987654321
```

**اردو:**

متعدد صارفین کو اجازت دینے کے لیے:
```bash
TELEGRAM_ALLOWED_USERS=123456789,987654321
```

**Roman Urdu:**

Mutaddid sarifeen ko ijazat dene ke liye:
```bash
TELEGRAM_ALLOWED_USERS=123456789,987654321
```

---

## 7. BotFather Additional Commands
## BotFather کے اضافی کمانڈز
## BotFather Ke Izafi Commands

**English:**

- `/setdescription` — set bot description
- `/setabouttext` — set about text
- `/setuserpic` — set bot profile photo
- `/mybots` — manage your bots
- `/deletebot` — delete a bot (careful!)

**اردو:**

- `/setdescription` — بوٹ کی تفصیل ترتیب دیں
- `/setabouttext` — about متن ترتیب دیں
- `/setuserpic` — بوٹ کی پروفائل تصویر ترتیب دیں
- `/mybots` — اپنے بوٹس کا انتظام کریں
- `/deletebot` — ایک بوٹ حذف کریں (احتیاط!)

**Roman Urdu:**

- `/setdescription` — Bot ki tafseel tarteeb dein
- `/setabouttext` — about matn tarteeb dein
- `/setuserpic` — Bot ki profile tasveer tarteeb dein
- `/mybots` — Apne bots ka intizam karein
- `/deletebot` — Ek bot hazf karein (ehtiyat!)

---

## 8. Privacy Settings
## رازداری کی ترتیبات
## Razdari Ki Tartibaat

**English:**

- `/setprivacy` in BotFather → set to **DISABLED** if you want bot to read all messages in groups
- Default: **ENABLED** (bot only sees commands and replies to it)

**اردو:**

- BotFather میں `/setprivacy` → **DISABLED** پر سیٹ کریں اگر آپ چاہتے ہیں کہ بوٹ گروپس میں تمام پیغامات پڑھے
- پہلے سے: **ENABLED** (بوٹ صرف کمانڈز اور اپنے جوابات دیکھتا ہے)

**Roman Urdu:**

- BotFather mein `/setprivacy` → **DISABLED** par set karein agar aap chahte hain ke bot groups mein tamam paighamat parhe
- Pehle se: **ENABLED** (bot sirf commands aur apne jawabat dekhta hai)
