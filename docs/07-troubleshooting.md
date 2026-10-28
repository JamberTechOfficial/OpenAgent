# 07 — Troubleshooting

> Real errors encountered during our setup session — with root causes and fixes.

---

## 1. Server Issues

| Error | Cause | Fix |
|---|---|---|
| Server froze completely, SSH timeout "banner exchange" | 1 GB RAM, no swap → OOM during git fetch (used 1.6 GB peak) | Add 4 GB swap BEFORE install |
| "Error establishing SSH connection" / "Connection timed out" | Server overloaded or crashed | Reboot from Oracle Cloud Console → Compute → Instance → Reboot |
| Server keeps freezing during heavy operations | RAM too low | Always add swap first; monitor with `free -h` during operations |

---

## 2. Installation Issues

| Error | Cause | Fix |
|---|---|---|
| `libatomic.so.1: cannot open shared object file` | libatomic1 not installed | `sudo apt-get install -y libatomic1` |
| `INSTALL_EXIT=True` — installer exited immediately | `</dev/null` in `bash -c` with heredoc killed stdin | Create a separate script file instead of inline bash |
| Install script hangs | Heavy download on slow server | Wait longer; or use screen: `screen -S install` |
| `hermes: command not found` after install | PATH not updated in current shell | Run `source ~/.bashrc` or use full path `~/.local/bin/hermes` |
| `--accept-hooks: unrecognized argument` | Flag belongs on hermes, not gateway install | Remove the `--accept-hooks` flag from `hermes gateway install` |

---

## 3. Gateway Issues

| Error | Cause | Fix |
|---|---|---|
| `service not installed` after running install | Manual gateway was still running | Run `hermes gateway stop` first, then `hermes gateway install` |
| `Gateway starting: deadline` when using `hermes -z` | Slow server startup (1 GB RAM) | Normal behavior; use Telegram to test instead |
| Gateway stops after SSH disconnect | Linger not enabled | Run `loginctl enable-linger ubuntu` |
| Gateway not starting on reboot | Linger not enabled | Run `loginctl enable-linger ubuntu` |

---

## 4. Telegram Issues

| Error | Cause | Fix |
|---|---|---|
| Bot doesn't respond | User never pressed START | Go to bot in Telegram → press START → send message |
| `Telegram: chat not found` in logs | User hasn't initiated conversation | User must send first message to bot |
| Bot token invalid | Wrong token copied | Get fresh token from @BotFather → /mybots |
| Messages delayed | Server under load | Check `free -h`; restart gateway if needed |

---

## 5. NVIDIA API Issues

| Error | Cause | Fix |
|---|---|---|
| 404 model not found | Model not available on free tier | Switch to `nvidia/nemotron-3-ultra-550b-a55b` |
| API timeout | Model overloaded or network issue | Retry; or switch to `minimaxai/minimax-m3.1-flash` |
| Invalid API key | Key not set correctly | Check `cat ~/.hermes/.env`; regenerate key at build.nvidia.com |
| Phone verification fails | Country not supported | Email help@build.nvidia.com; see NVIDIA guide |

---

## 6. SSH Issues

| Problem | Cause | Fix |
|---|---|---|
| `pkill -f <word>` killed SSH session | Pattern matched the SSH command itself | Use `pgrep -af <word>` to find PID first, then `kill <PID>` |
| SSH "banner exchange" timeout | Server overloaded | Wait for server to recover or reboot from Oracle Console |
| Permission denied (publickey) | Wrong key file or permissions | Use `-i /path/to/key.key`; check key permissions `chmod 600 key.key` |

---

## 7. Harmless Warnings (Ignore These)

```
cua-driver warning: libXi.so.6 not found → IGNORE (optional desktop tool)
Auxiliary Nous client unavailable → IGNORE (falls back to main model)
```

---

## 8. Quick Diagnostic Commands

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
