# Oracle Cloud Always Free — Complete Setup Guide

---

## 1. What is Oracle Cloud Always Free?

Oracle Cloud offers a **permanent free tier** — not a trial, not a limited period. These resources are yours forever at zero cost:

- **2x AMD Micro Instances** — 1 vCPU, 1 GB RAM each
- **OR 4x ARM Ampere A1 Cores** — up to 24 GB RAM total (e.g., 1 instance with 4 vCPUs + 24 GB RAM, or split across multiple VMs)
- **200 GB Block Storage** (total across all instances)
- **10 GB Object Storage**
- **Outbound data transfer:** 10 TB/month
- **Load Balancer, VCN, Monitoring** — also free

> **⚠️ IMPORTANT:** This is NOT a free trial. Oracle Always Free resources do **not** expire. Once created, your VM keeps running indefinitely for free.

---

## 2. Who Can Sign Up?

- Available in **most countries worldwide**
- You need:
  - ✅ A valid **email address**
  - ✅ A **mobile phone number** (for SMS OTP)
  - ✅ A **credit or debit card** (physical, internationally enabled) — charged $1 test only, which is automatically refunded

> **Note:** The $1 test charge is an authorization hold. It is reversed automatically within 3–7 business days. You will NOT be charged for Always Free usage.

---

## 3. Credit Cards Accepted — Country by Country

### Pakistan 🇵🇰

| Card Type | Works? | Notes |
|-----------|--------|-------|
| Standard Chartered (Credit/Debit) | ✅ Yes | Enable international transactions first |
| Meezan Bank (Credit/Debit) | ✅ Yes | Enable international e-commerce in app |
| HBL (Credit/Debit) | ✅ Yes | Call helpline or enable via app |
| Bank Alfalah (Credit/Debit) | ✅ Yes | Enable international transactions |
| UBL (Credit/Debit) | ✅ Yes | Enable in UBL Digital app |
| SadaPay Virtual Card | ❌ No | Virtual card BIN rejected |
| NayaPay Virtual Card | ❌ No | Virtual/prepaid card rejected |
| Any Prepaid Card | ❌ No | Not accepted |

**🔑 Pakistan Checklist:**
1. Use a **physical** credit or debit card (not virtual)
2. Enable **"International Transactions"** in your bank's app **before** applying
3. Ensure your billing address **exactly matches** your bank's registered address
4. Keep at least **$5 equivalent (PKR ~1,400+)** available for auth hold
5. Oracle charges **$1 test** — reversed automatically in 3–7 days

---

### India 🇮🇳

| Card Type | Works? | Notes |
|-----------|--------|-------|
| HDFC Credit Card | ✅ Yes | Best option |
| ICICI Credit Card | ✅ Yes | Works well |
| SBI Credit Card | ✅ Yes | Enable international payments |
| Axis Bank Credit Card | ✅ Yes | Works well |
| Kotak Credit Card | ✅ Yes | Works well |
| Debit Cards (any bank) | ⚠️ Sometimes | RBI e-mandate rules may block |

**🔑 India Checklist:**
1. **Prefer credit cards** over debit cards (RBI e-mandate issues with debit)
2. Enable **international transactions** in your banking app
3. Enable **international e-mandates** if available
4. Billing address must match bank records exactly

---

### UAE / Gulf 🇦🇪

| Card Type | Works? |
|-----------|--------|
| Emirates NBD | ✅ Yes |
| Abu Dhabi Commercial Bank (ADCB) | ✅ Yes |
| FAB (First Abu Dhabi Bank) | ✅ Yes |
| Most major Gulf bank cards | ✅ Yes |

- Most UAE/Gulf credit and debit cards work without issues
- Ensure international online payments are enabled

---

### Global 🌍

| Accepted | Not Accepted |
|----------|-------------|
| ✅ Visa (physical) | ❌ PayPal |
| ✅ Mastercard (physical) | ❌ Google Pay |
| ✅ American Express | ❌ Apple Pay |
| ✅ Major bank credit/debit cards | ❌ Prepaid cards |
| | ❌ Virtual cards |
| | ❌ Single-use cards |
| | ❌ Gift cards |

---

### Common Reasons for Card Failure

1. **Address mismatch** — Billing address must match your bank's registered address exactly (every word, every comma)
2. **International transactions disabled** — Must be enabled in your bank app/portal before attempting
3. **Prepaid or virtual card BIN** — Oracle's payment processor flags these automatically
4. **Insufficient balance** — Need at minimum ~$2–5 equivalent for the authorization hold
5. **Card issuer blocking** — Some banks auto-block foreign online charges; call your bank to whitelist Oracle

---

## 4. Best Server Location by Country

Choose your **Home Region** wisely — **it cannot be changed later!**

| Your Country | Recommended Region | Oracle Region Code | Est. Latency |
|---|---|---|---|
| Pakistan 🇵🇰 | Mumbai or Singapore | `ap-mumbai-1` | ~40–80 ms |
| India 🇮🇳 | Mumbai | `ap-mumbai-1` | ~10–30 ms |
| UAE / Gulf 🇦🇪 | Dubai or Frankfurt | `me-dubai-1` | ~20–40 ms |
| Turkey 🇹🇷 | Frankfurt | `eu-frankfurt-1` | ~20–40 ms |
| UK 🇬🇧 | London | `uk-london-1` | ~5–20 ms |
| Germany / Europe 🇩🇪 | Frankfurt | `eu-frankfurt-1` | ~10–20 ms |
| USA East 🇺🇸 | Ashburn, Virginia | `us-ashburn-1` | ~5 ms |
| USA West 🇺🇸 | Phoenix, Arizona | `us-phoenix-1` | ~5 ms |
| Australia 🇦🇺 | Sydney | `ap-sydney-1` | ~5–20 ms |
| China (users) 🇨🇳 | Singapore | `ap-singapore-1` | ~60–100 ms |

> **🔑 ARM Ampere A1 Availability:** A1 instances are NOT available in every region. Best regions for A1:
> - `ap-mumbai-1` ✅
> - `us-ashburn-1` ✅
> - `eu-frankfurt-1` ✅
> - `ap-singapore-1` ✅

---

## 5. Step-by-Step: Creating an Oracle Account

Follow these steps carefully to avoid common pitfalls:

### Step 1 — Go to Oracle Cloud
```
https://cloud.oracle.com
```
Click **"Start for free"**

### Step 2 — Enter Basic Info
- Your **country**
- Your **full name**
- Your **email address**

### Step 3 — Verify Email
- Check your inbox for Oracle's verification email
- Click the link inside

### Step 4 — Set Password
- Create a strong password (min 8 characters, mix of upper/lower/numbers/symbols)

### Step 5 — Choose Home Region ⚠️ CRITICAL
- Select the region **closest to you** (see table above)
- **This CANNOT be changed later — ever**
- For Pakistan: choose `ap-mumbai-1`
- For India: choose `ap-mumbai-1`
- For UAE: choose `me-dubai-1`

### Step 6 — Enter Payment Info
- Card number, expiry date, CVV
- Billing address — **must match your bank's address exactly**
- Oracle places a **$1 authorization hold** (automatically reversed in 3–7 days)
- If card fails: check international transactions are enabled, address matches

### Step 7 — Phone Verification
- Enter your mobile number
- Enter the SMS OTP received

### Step 8 — Account Created! 🎉
- You'll receive a confirmation email
- Wait a few minutes for account provisioning
- Login at `cloud.oracle.com`

---

## 6. Step-by-Step: Creating a Free VM Instance

### Step 1 — Login
Go to [cloud.oracle.com](https://cloud.oracle.com) and sign in.

### Step 2 — Navigate to Compute
```
☰ Menu → Compute → Instances → Create Instance
```

### Step 3 — Name Your Instance
- Enter a name, e.g.: `hermes-server`

### Step 4 — Choose OS Image
- Click **"Change image"**
- Select: **Canonical Ubuntu**
- Version: **Ubuntu 22.04** (recommended) or 20.04

### Step 5 — Choose Shape (CPU/RAM) ⚠️ Important
Click **"Change shape"**:

**For ARM Ampere A1 (Recommended — 4 vCPUs, 24 GB RAM FREE):**
```
Shape series: Ampere
Shape: VM.Standard.A1.Flex
OCPUs: 4
RAM: 24 GB
```

**For AMD Micro (Fallback — 1 vCPU, 1 GB RAM):**
```
Shape series: AMD
Shape: VM.Standard.E2.1.Micro
(No configuration needed — fixed size)
```

> **💡 Tip:** Start with Ampere A1 (4 OCPUs, 24 GB). If you get "Out of Capacity", try AMD Micro first, then retry A1 later.

### Step 6 — Networking
- Default VCN is fine for your first instance
- Leave defaults unless you know what you're doing

### Step 7 — SSH Keys ⚠️ Critical
- Select **"Generate a key pair for me"**
- Click **"Save private key"** — download and store safely!
- Click **"Save public key"** — download as backup
- **If you lose the private key, you cannot access your VM!**

### Step 8 — Boot Volume
- Default: **50 GB** (sufficient)
- Maximum free: 200 GB total across all instances
- Leave at 50 GB unless you need more

### Step 9 — Create!
- Click **"Create"**
- Wait 2–5 minutes for provisioning
- Status changes from `PROVISIONING` → `RUNNING`

---

## 7. After Instance Created

### Step 1 — Note the Public IP
- In instance details, find **"Public IP address"**
- Copy it — you'll need it for SSH

### Step 2 — Open Firewall Ports
By default, only port 22 (SSH) is open. For a server you need to open more ports:

1. Go to instance details → **"Subnet"** → **"Security List"**
2. Click **"Add Ingress Rules"**
3. Add rules as needed:

```
# Allow all traffic (easiest, less secure):
Source CIDR: 0.0.0.0/0
IP Protocol: All Protocols

# OR specific ports (more secure):
Source CIDR: 0.0.0.0/0
IP Protocol: TCP
Destination Port Range: 80    # HTTP
Destination Port Range: 443   # HTTPS
Destination Port Range: 8080  # Custom
```

> **⚠️ Also configure the instance's OS firewall (iptables/ufw) — OCI Security List alone is not enough!**

### Step 3 — SSH Into Your Instance

**On Linux/Mac:**
```bash
chmod 400 /path/to/your-private-key.key
ssh -i /path/to/your-private-key.key ubuntu@<YOUR-PUBLIC-IP>
```

**On Windows (PowerShell or CMD):**
```powershell
ssh -i C:\path\to\your-private-key.key ubuntu@<YOUR-PUBLIC-IP>
```

**On Windows (PuTTY):**
1. Convert `.key` to `.ppk` using PuTTYgen
2. Open PuTTY → Host: `ubuntu@<YOUR-PUBLIC-IP>`
3. Connection → SSH → Auth → Browse for `.ppk` file

### Step 4 — First Commands After Login
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Add swap (important for 1 GB RAM instances)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

---

## 8. Common Problems & Solutions

| Problem | Cause | Solution |
|---------|-------|----------|
| Card declined at signup | International transactions disabled | Enable in bank app before applying |
| "Address mismatch" error | Billing address ≠ bank records | Use exact address registered with bank |
| Home region capacity error | ARM instances full in chosen region | Try different region or use AMD Micro |
| SSH connection timeout | OCI firewall or OS firewall blocking | Check Security List AND ufw/iptables |
| Server freezes during install | RAM too low (1 GB AMD Micro) | Add swap file (see commands above) |
| "Out of capacity" on Ampere A1 | Very high demand in that region | See special note below ⬇️ |
| Cannot login after reboot | ufw blocked SSH | Always allow port 22 before enabling ufw |
| Instance terminated unexpectedly | Exceeded free tier / payment issue | Check Oracle billing console |

---

### ⚠️ Special Note: "Out of Capacity" for Ampere A1

This is **extremely common** and frustrating. Oracle's A1 ARM instances are in very high demand in popular regions. Many users have to try for **days or even weeks** before getting one.

**Tips to get an A1 instance:**

1. **Try at off-peak hours** — midnight to 4 AM local time often works better
2. **Try different Availability Domains** — in your region, switch between AD-1, AD-2, AD-3
3. **Start smaller** — try 1 OCPU + 6 GB RAM instead of 4 + 24 to improve chances
4. **Use OCI CLI to script retries:**

```bash
# Install OCI CLI on your local machine, then:
while true; do
  oci compute instance launch \
    --availability-domain "your-AD" \
    --compartment-id "your-compartment-ocid" \
    --shape "VM.Standard.A1.Flex" \
    --shape-config '{"ocpus": 4, "memoryInGBs": 24}' \
    --image-id "your-ubuntu-image-ocid" \
    --subnet-id "your-subnet-ocid" \
    --ssh-authorized-keys-file ~/.ssh/id_rsa.pub \
    --display-name "hermes-server" && break
  echo "Capacity unavailable. Retrying in 60 seconds..."
  sleep 60
done
```

5. **Try a different region** — if `ap-mumbai-1` is full, try `ap-singapore-1` or `us-ashburn-1`
6. **Don't give up** — availability opens up randomly as other users' instances are terminated

---

## Quick Reference Card

```
╔══════════════════════════════════════════════════════════════╗
║           ORACLE ALWAYS FREE — QUICK REFERENCE              ║
╠══════════════════════════════════════════════════════════════╣
║ Free Resources:                                              ║
║   • 4x ARM A1 Cores (24 GB RAM) OR 2x AMD Micro (1 GB ea)   ║
║   • 200 GB Block Storage | 10 GB Object Storage             ║
║                                                              ║
║ Pakistan Cards:  Standard Chartered, Meezan, HBL, Alfalah   ║
║ NOT Accepted:    SadaPay, NayaPay, any virtual/prepaid card  ║
║                                                              ║
║ Pakistan Region: ap-mumbai-1                                 ║
║ UAE Region:      me-dubai-1                                  ║
║                                                              ║
║ SSH Command:                                                 ║
║   ssh -i key.pem ubuntu@<YOUR-IP>                           ║
║                                                              ║
║ "Out of Capacity"? → Try midnight, try AD-2/AD-3, keep going ║
╚══════════════════════════════════════════════════════════════╝
```

---

*Next: [02-server-software-install.md](./02-server-software-install.md) — Installing and configuring the Hermes server software*
