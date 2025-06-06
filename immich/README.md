# 📸 Immich – Asmith Labs Configuration

This repo documents the setup of Immich in my TrueNAS SCALE home lab, including custom email templates and full SMTP/email infrastructure using Mailgun, ProtonMail, and Cloudflare.

---

## 🔧 Purpose

- Send branded, dark-mode email notifications from Immich using Mailgun
- Route email replies securely into ProtonMail using Cloudflare Email Routing
- Host and manage `.hbs` email templates styled to match Asmith Labs branding

---

## 📂 Directory Structure

```
immich/
├── email-templates/
│   ├── welcome.hbs
│   ├── album-invite.hbs
│   └── album-update.hbs
├── assets/
│   └── asmithlabs-logo.png
└── README.md
```

---

## 🧱 Immich Deployment (TrueNAS SCALE)

Immich was installed using the **TrueNAS SCALE App Store**.

📄 Installation guide used:  
🔗 https://immich.app/docs/install/truenas/

---

## ✉️ Email System Architecture

```
[Immich App]
   │
   ▼
[Mailgun SMTP]
   │
   ▼
[Cloudflare DNS + Email Routing]
   │
   ▼
[ProtonMail Inbox]
```

- **Mailgun** handles outbound mail (e.g., invites, album updates)
- **Cloudflare** manages DNS and forwards mail to ProtonMail
- **ProtonMail** serves as the final inbox for `admin@asmithlabs.com`

---

## 🛠️ Email Configuration

### ✅ ProtonMail (Inbound)

Configured to receive mail for `asmithlabs.com` using ProtonMail’s custom domain setup:

| Type | Name                     | Content                                       |
|------|--------------------------|-----------------------------------------------|
| MX   | asmithlabs.com           | `mail.protonmail.ch` (priority 10)            |
| MX   | asmithlabs.com           | `mailsec.protonmail.ch` (priority 10)         |
| TXT  | asmithlabs.com           | `protonmail-verification=...`                 |
| CNAME| protonmail._domainkey    | `protonmail.domainkey.d4...` (DKIM 1)         |
| CNAME| protonmail2._domainkey   | `protonmail2.domainkey.d4...` (DKIM 2)        |
| CNAME| protonmail3._domainkey   | `protonmail3.domainkey.d4...` (DKIM 3)        |
| TXT  | asmithlabs.com           | `include:_spf.protonmail.ch`                  |

---

### ✅ Cloudflare (DNS + Forwarding)

Cloudflare is used for:
- DNS management for `asmithlabs.com`
- Email forwarding from `admin@asmithlabs.com` to ProtonMail

| Type | Name              | Content                                 |
|------|-------------------|------------------------------------------|
| MX   | asmithlabs.com    | `route1.mx.cloudflare.net` (priority 12) |
| MX   | asmithlabs.com    | `route2.mx.cloudflare.net` (priority 12) |
| MX   | asmithlabs.com    | `route3.mx.cloudflare.net` (priority 23) |
| TXT  | asmithlabs.com    | `include:_spf.mx.cloudflare.net`         |

---

### ✅ Mailgun (SMTP Outbound)

Used to send mail from Immich (`admin@asmithlabs.com`):

| Type | Name          | Content                              |
|------|---------------|---------------------------------------|
| MX   | `mg`          | `mxa.mailgun.org` (priority 10)       |
| MX   | `mg`          | `mxb.mailgun.org` (priority 10)       |
| TXT  | `mg`          | `v=spf1 include:mailgun.org ~all`     |
| TXT  | `_dmarc.mg`    | `v=DMARC1; p=none; pct=100; rua=...` |
| TXT  | `pic._domainkey.mg` | (DKIM key from Mailgun)           |

---

### ✅ Unified SPF Record

Only one SPF record is valid per domain. The unified SPF for your domain:

```txt
v=spf1 include:mailgun.org include:_spf.mx.cloudflare.net include:_spf.protonmail.ch ~all
```

This record:
- Authorizes **Mailgun** to send
- Authorizes **Cloudflare** to forward
- Authorizes **ProtonMail** to send replies

---

## 💌 Email Templates

Templates were created using HTML + Handlebars (`.hbs`) with dark-mode support and pasted directly into Immich via:

> Admin UI → Settings → Email Templates

### Templates and Variables:

- `welcome.hbs`:  
  `{username}, {password}, {displayName}, {baseUrl}`

- `album-invite.hbs`:  
  `{senderName}, {recipientName}, {albumId}, {albumName}, {baseUrl}`

- `album-update.hbs`:  
  `{recipientName}, {albumId}, {albumName}, {baseUrl}`

---

## 🖼️ Branding

- Font: **Arial**
- Background: `#121212`
- Text: `#e0e0e0`
- Accent: `#40e0d0`
- Logo: 

     ![Logo](https://i.imgur.com/hkU8OiG.png)
- Email signature block:

```
Antonio Smith, MD  
Founder, Asmith Labs  
admin@asmithlabs.com  
https://asmithlabs.com  
```

---
---

## 🔁 Snapshot & Backup Strategy

Immich datasets are backed up using **TrueNAS ZFS snapshots** and replication to an external 8TB USB pool (`MyBookPool`).

### 📂 Source Dataset
```
/mnt/samsungssdpool/immich
```

### 💾 Destination Pool
```
/mnt/MyBookPool/immich
```

### 🔧 Snapshot + Replication Setup

- **Method**: TrueNAS Replication Task Wizard
- **Type**: Push replication from main pool → MyBookPool
- **Schedule**: Daily at 2 AM
- **Retention**: Last 7 snapshots
- **Recursive**: Enabled (includes photos, db, config if nested)

### 🧪 Recovery Workflow

To recover from backup:
1. Clone latest snapshot from `/mnt/MyBookPool/immich`
2. Replace or remount as live dataset
3. Restart Immich app if needed

---


## 📄 License

This project is licensed under the **MIT License**.

