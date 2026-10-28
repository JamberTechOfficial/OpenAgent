# 06 — Telegram Bot Setup

---

## 1. What You Need

- A Telegram account
- A server (see other guides)

---

## 2. Create a Telegram Bot via @BotFather

1. Open Telegram
2. Search for: **@BotFather** → https://telegram.me/BotFather
3. Press START
4. Send: `/newbot`
5. Enter bot name: (e.g., "My Hermes Bot")
6. Enter bot username: (must end in `bot`, e.g., `myhermesbot` or `my_hermes_bot`)
7. BotFather replies with your **Bot Token** — looks like: `1234567890:AAFxxxxx...`
8. SAVE this token — you'll need it

---

## 3. Get Your Telegram User ID

1. Open Telegram
2. Search for: **@userinfobot** → https://telegram.me/userinfobot
3. Press START
4. It replies with your user info including your **numeric User ID** (e.g., `<your-user-id>`)
5. SAVE this ID

---

## 4. Add to Hermes .env

```bash
TELEGRAM_BOT_TOKEN=<your-bot-token-from-botfather>
TELEGRAM_ALLOWED_USERS=<your-numeric-user-id>
```

---

## 5. Test the Bot

1. The bot CANNOT message you first — you must initiate
2. Find your bot in Telegram (search @yourbotusername)
3. Press START
4. Send any message
5. If Hermes gateway is running, you'll get a reply!

---

## 6. Multiple Allowed Users

To allow multiple users:
```bash
TELEGRAM_ALLOWED_USERS=123456789,987654321
```

---

## 7. BotFather Additional Commands

- `/setdescription` — set bot description
- `/setabouttext` — set about text
- `/setuserpic` — set bot profile photo
- `/mybots` — manage your bots
- `/deletebot` — delete a bot (careful!)

---

## 8. Privacy Settings

- `/setprivacy` in BotFather → set to **DISABLED** if you want bot to read all messages in groups
- Default: **ENABLED** (bot only sees commands and replies to it)
