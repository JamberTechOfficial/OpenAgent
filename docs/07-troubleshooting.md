# 07 — Troubleshooting
# مسائل کا حل
# Masail Ka Hal

> Real errors encountered during our setup session — with root causes and fixes.
> سیٹ اپ سیشن کے دوران پیش آنے والی حقیقی خرابیاں — بنیادی وجوہات اور حل کے ساتھ۔
> Setup session ke dauran pesh aane wali haqeeqi kharabiyan — bunyadi wajuhaat aur hal ke saath.

---

## 1. Server Issues
## سرور کے مسائل
## Server Ke Masail

**English:**

| Error | Cause | Fix |
|---|---|---|
| Server froze completely, SSH timeout "banner exchange" | 1 GB RAM, no swap → OOM during git fetch (used 1.6 GB peak) | Add 4 GB swap BEFORE install |
| "Error establishing SSH connection" / "Connection timed out" | Server overloaded or crashed | Reboot from Oracle Cloud Console → Compute → Instance → Reboot |
| Server keeps freezing during heavy operations | RAM too low | Always add swap first; monitor with `free -h` during operations |

**اردو:**

| خرابی | وجہ | حل |
|---|---|---|
| سرور مکمل طور پر جم گیا، SSH ٹائم آؤٹ "banner exchange" | 1 GB RAM، کوئی swap نہیں → git fetch کے دوران OOM (1.6 GB تک پہنچا) | انسٹال سے پہلے 4 GB swap شامل کریں |
| "Error establishing SSH connection" / "Connection timed out" | سرور اوورلوڈ یا کریش | Oracle Cloud Console → Compute → Instance → Reboot سے ری بوٹ کریں |
| بھاری آپریشنز کے دوران سرور بار بار جمتا ہے | RAM بہت کم ہے | ہمیشہ پہلے swap شامل کریں؛ آپریشنز کے دوران `free -h` سے مانیٹر کریں |

**Roman Urdu:**

| Kharabi | Wajah | Hal |
|---|---|---|
| Server mukammal tor par jam gaya, SSH timeout "banner exchange" | 1 GB RAM, koi swap nahi → git fetch ke dauran OOM (1.6 GB tak pohuncha) | Install se pehle 4 GB swap shamil karein |
| "Error establishing SSH connection" / "Connection timed out" | Server overload ya crash | Oracle Cloud Console → Compute → Instance → Reboot se reboot karein |
| Bhari operations ke dauran server baar baar jamta hai | RAM bohat kam hai | Hamesha pehle swap shamil karein; operations ke dauran `free -h` se monitor karein |

---

## 2. Installation Issues
## انسٹالیشن کے مسائل
## Installation Ke Masail

**English:**

| Error | Cause | Fix |
|---|---|---|
| `libatomic.so.1: cannot open shared object file` | libatomic1 not installed | `sudo apt-get install -y libatomic1` |
| `INSTALL_EXIT=True` — installer exited immediately | `</dev/null` in `bash -c` with heredoc killed stdin | Create a separate script file instead of inline bash |
| Install script hangs | Heavy download on slow server | Wait longer; or use screen: `screen -S install` |
| `hermes: command not found` after install | PATH not updated in current shell | Run `source ~/.bashrc` or use full path `~/.local/bin/hermes` |
| `--accept-hooks: unrecognized argument` | Flag belongs on hermes, not gateway install | Remove the `--accept-hooks` flag from `hermes gateway install` |

**اردو:**

| خرابی | وجہ | حل |
|---|---|---|
| `libatomic.so.1: cannot open shared object file` | libatomic1 انسٹال نہیں | `sudo apt-get install -y libatomic1` |
| `INSTALL_EXIT=True` — انسٹالر فوری طور پر بند ہو گیا | `bash -c` میں `</dev/null` کے ساتھ heredoc نے stdin ختم کر دیا | inline bash کی جگہ ایک الگ اسکرپٹ فائل بنائیں |
| انسٹال اسکرپٹ رک جاتی ہے | سست سرور پر بھاری ڈاؤنلوڈ | زیادہ انتظار کریں؛ یا screen استعمال کریں: `screen -S install` |
| انسٹال کے بعد `hermes: command not found` | موجودہ شیل میں PATH اپ ڈیٹ نہیں ہوا | `source ~/.bashrc` چلائیں یا پورا راستہ استعمال کریں `~/.local/bin/hermes` |
| `--accept-hooks: unrecognized argument` | یہ فلیگ hermes پر لگتا ہے، gateway install پر نہیں | `hermes gateway install` سے `--accept-hooks` فلیگ ہٹائیں |

**Roman Urdu:**

| Kharabi | Wajah | Hal |
|---|---|---|
| `libatomic.so.1: cannot open shared object file` | libatomic1 install nahi | `sudo apt-get install -y libatomic1` |
| `INSTALL_EXIT=True` — installer fori tor par band ho gaya | `bash -c` mein `</dev/null` ke saath heredoc ne stdin khatam kar diya | inline bash ki jagah ek alag script file banayein |
| Install script ruk jati hai | Sust server par bhari download | Zyada intezar karein; ya screen istemaal karein: `screen -S install` |
| Install ke baad `hermes: command not found` | Maujuda shell mein PATH update nahi hua | `source ~/.bashrc` chalayein ya poora rasta istemaal karein `~/.local/bin/hermes` |
| `--accept-hooks: unrecognized argument` | Yeh flag hermes par lagta hai, gateway install par nahi | `hermes gateway install` se `--accept-hooks` flag hatayein |

---

## 3. Gateway Issues
## گیٹ وے کے مسائل
## Gateway Ke Masail

**English:**

| Error | Cause | Fix |
|---|---|---|
| `service not installed` after running install | Manual gateway was still running | Run `hermes gateway stop` first, then `hermes gateway install` |
| `Gateway starting: deadline` when using `hermes -z` | Slow server startup (1 GB RAM) | Normal behavior; use Telegram to test instead |
| Gateway stops after SSH disconnect | Linger not enabled | Run `loginctl enable-linger ubuntu` |
| Gateway not starting on reboot | Linger not enabled | Run `loginctl enable-linger ubuntu` |

**اردو:**

| خرابی | وجہ | حل |
|---|---|---|
| انسٹال چلانے کے بعد `service not installed` | میڈمیوال گیٹ وے ابھی بھی چل رہا تھا | پہلے `hermes gateway stop` چلائیں، پھر `hermes gateway install` |
| `hermes -z` استعمال کرتے وقت `Gateway starting: deadline` | سست سرور اسٹارٹ اپ (1 GB RAM) | عام رویہ؛ اس کی بجائے ٹیلیگرام سے ٹیسٹ کریں |
| SSH ڈسکنیکٹ کے بعد گیٹ وے رک جاتا ہے | Linger فعال نہیں | `loginctl enable-linger ubuntu` چلائیں |
| ری بوٹ پر گیٹ وے شروع نہیں ہوتا | Linger فعال نہیں | `loginctl enable-linger ubuntu` چلائیں |

**Roman Urdu:**

| Kharabi | Wajah | Hal |
|---|---|---|
| Install chalane ke baad `service not installed` | Manual gateway abhi bhi chal raha tha | Pehle `hermes gateway stop` chalayein, phir `hermes gateway install` |
| `hermes -z` istemaal karte waqt `Gateway starting: deadline` | Sust server startup (1 GB RAM) | Aam rawiya; iski bajaye Telegram se test karein |
| SSH disconnect ke baad gateway ruk jata hai | Linger faaal nahi | `loginctl enable-linger ubuntu` chalayein |
| Reboot par gateway shuru nahi hota | Linger faaal nahi | `loginctl enable-linger ubuntu` chalayein |

---

## 4. Telegram Issues
## ٹیلیگرام کے مسائل
## Telegram Ke Masail

**English:**

| Error | Cause | Fix |
|---|---|---|
| Bot doesn't respond | User never pressed START | Go to bot in Telegram → press START → send message |
| `Telegram: chat not found` in logs | User hasn't initiated conversation | User must send first message to bot |
| Bot token invalid | Wrong token copied | Get fresh token from @BotFather → /mybots |
| Messages delayed | Server under load | Check `free -h`; restart gateway if needed |

**اردو:**

| خرابی | وجہ | حل |
|---|---|---|
| بوٹ جواب نہیں دیتا | صارف نے START نہیں دبایا | ٹیلیگرام میں بوٹ پر جائیں → START دبائیں → پیغام بھیجیں |
| لاگز میں `Telegram: chat not found` | صارف نے گفتگو شروع نہیں کی | صارف کو بوٹ کو پہلا پیغام بھیجنا ہوگا |
| بوٹ ٹوکن غلط ہے | غلط ٹوکن کاپی کیا | @BotFather → /mybots سے نیا ٹوکن حاصل کریں |
| پیغامات میں تاخیر | سرور لوڈ میں ہے | `free -h` چیک کریں؛ ضرورت ہو تو gateway ری اسٹارٹ کریں |

**Roman Urdu:**

| Kharabi | Wajah | Hal |
|---|---|---|
| Bot jawab nahi deta | Sarif ne START nahi dabaya | Telegram mein bot par jayein → START dabaein → paigham bhejein |
| Logs mein `Telegram: chat not found` | Sarif ne guftagu shuru nahi ki | Sarif ko bot ko pehla paigham bhejna hoga |
| Bot token ghalat hai | Ghalat token copy kiya | @BotFather → /mybots se naya token hasil karein |
| Paighamat mein takheer | Server load mein hai | `free -h` check karein; zaroorat ho to gateway restart karein |

---

## 5. NVIDIA API Issues
## NVIDIA API کے مسائل
## NVIDIA API Ke Masail

**English:**

| Error | Cause | Fix |
|---|---|---|
| 404 model not found | Model not available on free tier | Switch to `nvidia/nemotron-3-ultra-550b-a55b` |
| API timeout | Model overloaded or network issue | Retry; or switch to `minimaxai/minimax-m3.1-flash` |
| Invalid API key | Key not set correctly | Check `cat ~/.hermes/.env`; regenerate key at build.nvidia.com |
| Phone verification fails | Country not supported | Email help@build.nvidia.com; see NVIDIA guide |

**اردو:**

| خرابی | وجہ | حل |
|---|---|---|
| 404 model not found | فری ٹیئر پر ماڈل دستیاب نہیں | `nvidia/nemotron-3-ultra-550b-a55b` پر سوئچ کریں |
| API ٹائم آؤٹ | ماڈل اوورلوڈ یا نیٹ ورک کا مسئلہ | دوبارہ کوشش کریں؛ یا `minimaxai/minimax-m3.1-flash` پر سوئچ کریں |
| Invalid API key | کلید صحیح طریقے سے سیٹ نہیں کی گئی | `cat ~/.hermes/.env` چیک کریں؛ build.nvidia.com پر کلید دوبارہ بنائیں |
| فون تصدیق ناکام ہوتی ہے | ملک سپورٹ نہیں ہے | help@build.nvidia.com کو ای میل کریں؛ NVIDIA گائیڈ دیکھیں |

**Roman Urdu:**

| Kharabi | Wajah | Hal |
|---|---|---|
| 404 model not found | Free tier par model dastiyab nahi | `nvidia/nemotron-3-ultra-550b-a55b` par switch karein |
| API timeout | Model overload ya network ka masla | Dobara koshish karein; ya `minimaxai/minimax-m3.1-flash` par switch karein |
| Invalid API key | Kulid sahih tareeqe se set nahi ki gayi | `cat ~/.hermes/.env` check karein; build.nvidia.com par kulid dobara banayein |
| Phone tasdeeq nakaam hoti hai | Mulk support nahi hai | help@build.nvidia.com ko email karein; NVIDIA guide dekhein |

---

## 6. SSH Issues
## SSH کے مسائل
## SSH Ke Masail

**English:**

| Problem | Cause | Fix |
|---|---|---|
| `pkill -f <word>` killed SSH session | Pattern matched the SSH command itself | Use `pgrep -af <word>` to find PID first, then `kill <PID>` |
| SSH "banner exchange" timeout | Server overloaded | Wait for server to recover or reboot from Oracle Console |
| Permission denied (publickey) | Wrong key file or permissions | Use `-i /path/to/key.key`; check key permissions `chmod 600 key.key` |

**اردو:**

| مسئلہ | وجہ | حل |
|---|---|---|
| `pkill -f <word>` نے SSH سیشن ختم کر دیا | پیٹرن نے SSH کمانڈ سے میچ کیا | پہلے PID تلاش کرنے کے لیے `pgrep -af <word>` استعمال کریں، پھر `kill <PID>` |
| SSH "banner exchange" ٹائم آؤٹ | سرور اوورلوڈ | سرور کے ٹھیک ہونے کا انتظار کریں یا Oracle Console سے ری بوٹ کریں |
| Permission denied (publickey) | غلط کلید فائل یا اجازتیں | `-i /path/to/key.key` استعمال کریں؛ کلید اجازتیں چیک کریں `chmod 600 key.key` |

**Roman Urdu:**

| Masla | Wajah | Hal |
|---|---|---|
| `pkill -f <word>` ne SSH session khatam kar diya | Pattern ne SSH command se match kiya | Pehle PID talash karne ke liye `pgrep -af <word>` istemaal karein, phir `kill <PID>` |
| SSH "banner exchange" timeout | Server overload | Server ke theek hone ka intezar karein ya Oracle Console se reboot karein |
| Permission denied (publickey) | Ghalat kulid file ya ijazatein | `-i /path/to/key.key` istemaal karein; kulid ijazatein check karein `chmod 600 key.key` |

---

## 7. Harmless Warnings (Ignore These)
## بے ضرر انتباہات (انہیں نظرانداز کریں)
## Be Zarar Intibahaat (Inhein Nazar Andaz Karein)

**English:**

```
cua-driver warning: libXi.so.6 not found → IGNORE (optional desktop tool)
Auxiliary Nous client unavailable → IGNORE (falls back to main model)
```

**اردو:**

```
cua-driver warning: libXi.so.6 not found → نظرانداز کریں (اختیاری ڈیسک ٹاپ ٹول)
Auxiliary Nous client unavailable → نظرانداز کریں (مرکزی ماڈل پر واپس جاتا ہے)
```

**Roman Urdu:**

```
cua-driver warning: libXi.so.6 not found → Nazar andaz karein (ikhtiyari desktop tool)
Auxiliary Nous client unavailable → Nazar andaz karein (markazi model par wapas jata hai)
```

---

## 8. Quick Diagnostic Commands
## فوری تشخیصی کمانڈز
## Fori Tashkhisi Commands

**English:**

```bash
# Check gateway status
~/.local/bin/hermes gateway status

# View recent logs
journalctl --user -u hermes-gateway -n 50 --no-pager

# Check memory
free -h

# Check disk
df -h

# Check running services
systemctl --user list-units --type=service

# Check swap
swapon --show

# Check fail2ban
sudo fail2ban-client status sshd
```

**اردو:**

```bash
# گیٹ وے اسٹیٹس چیک کریں
~/.local/bin/hermes gateway status

# حالیہ لاگز دیکھیں
journalctl --user -u hermes-gateway -n 50 --no-pager

# میموری چیک کریں
free -h

# ڈسک چیک کریں
df -h

# چلتی ہوئی سروسز چیک کریں
systemctl --user list-units --type=service

# Swap چیک کریں
swapon --show

# Fail2ban چیک کریں
sudo fail2ban-client status sshd
```

**Roman Urdu:**

```bash
# Gateway status check karein
~/.local/bin/hermes gateway status

# Haaliya logs dekhein
journalctl --user -u hermes-gateway -n 50 --no-pager

# Memory check karein
free -h

# Disk check karein
df -h

# Chalti hui services check karein
systemctl --user list-units --type=service

# Swap check karein
swapon --show

# Fail2ban check karein
sudo fail2ban-client status sshd
```
