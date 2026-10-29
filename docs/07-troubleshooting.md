# 07 — Troubleshooting Guide

> Real issues encountered during production setup of OraHermes Agent, Web Dashboard, and reverse proxy — with exact root causes and tested fixes.

---

## 1. Web Dashboard & Reverse Proxy Issues

| Symptom | Cause | Solution |
|---|---|---|
| `HTTP 401 Unauthorized` | HTTP Basic Auth credential mismatch | Reset password using `sudo htpasswd -b /etc/nginx/.htpasswd admin <dashboard-password>`. |
| `HTTP 405 Method Not Allowed` on `curl -I` | SPA router serves GET for index but rejects HEAD requests | Add `error_page 405 =200 @handle_head;` in Nginx site config with `@handle_head { default_type text/html; return 200; }`. |
| `FastAPI Host Header Violation` (GHSA-ppp5-vxwm-4cf7) | Loopback host middleware expects `Host: 127.0.0.1` | In Nginx reverse proxy configuration, set `proxy_set_header Host 127.0.0.1;` and pass original client host in `X-Forwarded-Host $host;`. |
| Web Dashboard fails to start | Missing `web_dist` frontend bundle | Run dashboard with `--skip-build` if production assets are already in `hermes_cli/web_dist/`. |
| Browser shows SSL warning | Self-signed certificate in use | Standard behavior on self-signed certs. Click "Advanced" -> "Proceed", or configure Let's Encrypt Certbot with a custom domain. |

---

## 2. Server Performance & Memory Issues

| Symptom | Cause | Solution |
|---|---|---|
| Server freezes completely during package build | 1 GB RAM exhausted (no swap) | Allocate a 4 GB swap file (`sudo fallocate -l 4G /swapfile`) before heavy operations. |
| Memory pressure / high RAM usage | Desktop GUI packages (XRDP, XFCE4, Xorg) running | Purge GUI stack: `sudo apt-get purge -y xrdp xorg 'xfce4*' 'lightdm*' 'gdm3*' && sudo apt-get autoremove -y --purge`. |
| SSH disconnects during background commands | Session terminated by hangup | Enable systemd lingering: `sudo loginctl enable-linger ubuntu` and manage processes with systemd units. |

---

## 3. Telegram Messaging Gateway Issues

| Symptom | Cause | Solution |
|---|---|---|
| Bot does not reply to messages | User hasn't initiated chat | In Telegram, open the bot profile and tap **START** first. |
| `[Telegram] Unauthorized: bot token invalid` | Typo in token copied from BotFather | Re-verify `TELEGRAM_BOT_TOKEN` in `~/.hermes/.env` and restart `systemctl --user restart hermes-gateway`. |
| Bot ignores messages from user | User ID not whitelisted | Query `@userinfobot` for numeric user ID and add to `TELEGRAM_ALLOWED_USERS` in `~/.hermes/.env`. |
| Gateway stops when user disconnects SSH | User lingering disabled | Run `sudo loginctl enable-linger ubuntu`. |

---

## 4. NVIDIA NIM API Issues

| Symptom | Cause | Solution |
|---|---|---|
| `404 Function Not Found for Account` | Selected model is unavailable on current account tier | Use confirmed model `nvidia/nemotron-3-ultra-550b-a55b` or backup `minimaxai/minimax-m3.1-flash`. |
| `401 Unauthorized` | Invalid or expired API key | Check key at `https://build.nvidia.com` and update `NVIDIA_API_KEY` in `~/.hermes/.env`. |
| SMS verification fails during account creation | International SMS gateway filtering | Contact `help@build.nvidia.com` with subject `Manual API Key Activation Request - Regional SMS Failure`. |

---

## 5. Quick Diagnostic Commands

```bash
# Check Telegram Gateway status
systemctl --user status hermes-gateway

# Check Web Dashboard status
sudo systemctl status hermes-dashboard

# Check Nginx status and syntax
sudo systemctl status nginx
sudo nginx -t

# Check active listening ports
sudo ss -tlnp

# Verify memory and swap
free -h

# Check fail2ban jails
sudo fail2ban-client status sshd
```

---

*OraHermes Community Agent | Production Troubleshooting Guide*
