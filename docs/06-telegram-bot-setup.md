# 06 — Telegram Bot Gateway Setup for OraHermes

---

## 1. What You Need

- A Telegram account on mobile or desktop
- An active Linux server with `orahermes-agent` deployed (see `03-hermes-agent-setup.md`)

---

## 2. Create a Telegram Bot via @BotFather

1. Open Telegram and search for **@BotFather** (`https://telegram.me/BotFather`).
2. Press **START** or send `/start`.
3. Send: `/newbot`.
4. Enter bot display name: e.g. `OraHermes Community Agent`.
5. Enter bot username (must end in `bot`): e.g. `jtcommunitybot` or `my_orahermes_bot`.
6. BotFather will reply with your **Bot Token** in the format `1234567890:AAFxxxxx...`.
7. Save this token as `<your-telegram-bot-token>`.

---

## 3. Get Your Telegram User ID

For security, OraHermes restricts bot command execution strictly to authorized user IDs:

1. In Telegram, search for **@userinfobot** (`https://telegram.me/userinfobot`).
2. Press **START**.
3. The bot replies with your profile details, including your numeric **Id** (e.g. `6040662896`).
4. Save this ID as `<your-telegram-user-id>`.

---

## 4. Configure `~/.hermes/.env`

Add your credentials to the agent environment file:

```bash
cat >> ~/.hermes/.env << 'EOF'
TELEGRAM_BOT_TOKEN=<your-telegram-bot-token>
TELEGRAM_ALLOWED_USERS=<your-telegram-user-id>
EOF

chmod 600 ~/.hermes/.env
```

If multiple users are authorized to interact with the bot, provide comma-separated numeric IDs:
```bash
TELEGRAM_ALLOWED_USERS=<user-id-1>,<user-id-2>
```

---

## 5. Start and Verify the Gateway

```bash
# Restart gateway to load new credentials
systemctl --user restart hermes-gateway

# Verify status
systemctl --user status hermes-gateway

# Check journal logs for connection confirmation
journalctl --user -u hermes-gateway -n 20 --no-pager
```

Expected log output:
```
[Telegram] Connected to Telegram (polling mode)
[Gateway] Listening for authorized incoming messages...
```

---

## 6. Initiating Conversation

> [!IMPORTANT]
> Telegram bots cannot initiate contact with users. You must open your bot in Telegram and press **START** first before sending prompts.

1. Search for your bot's username in Telegram.
2. Tap **START**.
3. Send: `Assalam o Alaikum! Who are you?`
4. The bot will respond in seconds using the configured NVIDIA NIM model.

---

*OraHermes Community Agent | Telegram Integration*
