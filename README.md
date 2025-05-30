# home_lab

Documenting my home lab journey!

Home NAS Setup Documentation

## 1. Overview
Learn networking concepts and basics of web development through the
implementation of a home lab. 

## 2. Hardware Components

| Component             | Purpose                         | Notes                                      |
|-----------------------|---------------------------------|--------------------------------------------|
| Lenovo M920q          | NAS host                        | Low power, business-class reliability      |
|- 2TB SSD              | OS + cache drive                | TrueNAS SCALE installed                    |
|- 8TB External USB HDD | Primary data storage            | Formatted as EXT4 for stability            |
| Raspberry Pi          | Home Assistant hub              | LAN integration only                       |
| YubiKey               | Authentication device           | Used for SSH key-based access              |

## 3. OS and Software
- Chosen OS: **TrueNAS SCALE**
- TrueNAS SCALE has a low barrier to entry in terms of installation,
    interaction via GUI and adequate selection of native applicatons. KVM under
    the hood also allows for minor implementation of virualization through
    docker containers. 
- contenders included proxmox and Ubuntu server. proxmox was attractive due to
   the granularity it provides when distributing CPU resources. However, I did
   not want to compromise my introduction to home networking by overexposure to
   complexity. 
- TrueNAS SCALE is currently running syncthing to sync my notes via obsidian
    with my macbook pro and iphone through SMB shares.I am also runnign immich
    to offload end devices and for backups.
    
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
