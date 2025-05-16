# 🏠 Home NAS Setup – To-Do List

## 🖥️ 1. Base System Setup
- [ ] Install **TrueNAS SCALE** on the 2TB SSD
- [ ] Format the 8TB external USB drive as **EXT4**
- [ ] Create a **data pool** in TrueNAS using the external drive
- [ ] Create **SMB shares** for LAN file access
- [ ] Assign a **static IP address** to the NAS

## 🔐 2. Security Hardening
- [ ] Create strong admin credentials for TrueNAS
- [ ] Enable and configure **SSH access using YubiKey**
  - [ ] Enable `sshd`
  - [ ] Use public key authentication with YubiKey
- [ ] Configure **firewall rules**: block WAN, allow LAN only
- [ ] Install or enable **fail2ban** (brute force protection)
- [ ] Disable unused services (FTP, NFS, etc.)

## 🌐 3. Secure Remote Access
- [ ] Set up **WireGuard VPN** or **OpenVPN**
  - [ ] Install VPN server on NAS or router
  - [ ] Use key-based authentication
  - [ ] Forward minimal ports via router
- [ ] Test remote access (e.g., mobile hotspot)
- [ ] Enable audit logging and alerts for remote access
- [ ] (Optional) Enable 2FA for TrueNAS web UI (if available)

## 📦 4. Services & Integration
- [ ] Configure **SMART monitoring** and email alerts
- [ ] Write backup scripts (rsync to external/cloud)
- [ ] (Optional) Deploy containers:
  - [ ] Nextcloud
  - [ ] Syncthing
  - [ ] Pi-hole
- [ ] Integrate NAS health with **Home Assistant**

## 🧾 5. Documentation
- [ ] Create `README.md` with system overview
- [ ] List hardware components and rationale
- [ ] Document file system and storage configuration
- [ ] Describe security setup and remote access configuration
- [ ] Include sample config files: `.vimrc`, `fstab`, backup scripts
- [ ] Add screenshots (TrueNAS dashboard, share setup, etc.)
- [ ] (Optional) Include notes on clinical relevance (PHI, HIPAA, etc.)

## 🚀 6. Future Enhancements
- [ ] Add internal SATA drive for ZFS pool
- [ ] Enable and automate snapshots
- [ ] Set up offsite encrypted backups
- [ ] Implement role-based user access controls
