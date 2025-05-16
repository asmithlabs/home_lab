# home_lab
Documenting my home lab journey!

Home NAS Setup Documentation

## 1. Overview
Brief summary of the purpose and goals of the NAS system.

## 2. Hardware Components

| Component            | Purpose                         | Notes                                      |
|---------------------|----------------------------------|--------------------------------------------|
| Lenovo M920q         | NAS host                        | Low power, business-class reliability      |
| 2TB SSD              | OS + cache drive                | TrueNAS SCALE installed                    |
| 8TB External USB HDD | Primary data storage            | Formatted as EXT4 for stability            |
| Raspberry Pi         | Home Assistant hub              | LAN integration only                       |
| YubiKey              | Authentication device           | Used for SSH key-based access              |

## 3. OS and Software
- Chosen OS: **TrueNAS SCALE**
- Justification over alternatives (Unraid, OMV, etc.)
- Overview of installed services

## 4. File System & Storage
- Layout of drives and partitions
- File system choices (EXT4 vs ZFS)
- Mount points and sharing setup
- Snapshot/backup strategy

## 5. Network Configuration
- Static IP setup
- LAN-only access model
- VPN tunnel setup for secure remote access

## 6. Security Measures
- SSH hardening with YubiKey
- Local-only web access
- Fail2ban/firewall rules
- Disabled unused services

## 7. Service Integration
- SMB/NFS file shares
- Optional: Docker containers (Nextcloud, etc.)
- Home Assistant integration (system uptime, health, etc.)

## 8. Challenges & Fixes
- Problems encountered (e.g., ZFS vs USB)
- Solutions implemented

## 9. Future Plans
- ZFS pool with internal disks
- Cloud or offsite backups
- Role-based access and encryption

## 10. Appendix
- Config files (`.vimrc`, `fstab`, scripts)
- Screenshots
- References or links to docs/tools used
