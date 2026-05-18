# 🎮 Build Hub

![Build Hub](https://img.shields.io/badge/Build_Hub-v1.6-E03060?style=for-the-badge)
![Games](https://img.shields.io/badge/Games-3-E8A820?style=for-the-badge&logo=steam&logoColor=white)
![Builds](https://img.shields.io/badge/Builds-8-2FB8B4?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-4CAF50?style=for-the-badge)
![iPad](https://img.shields.io/badge/iPad_Ready-%E2%9C%93-E03060?style=for-the-badge&logo=apple&logoColor=white)
![Self-Hosted](https://img.shields.io/badge/Self--Hosted-Proxmox-E8A820?style=for-the-badge)

> **A personal gaming build reference hub — optimized for iPad, self-hosted on Proxmox.**
> *The Division 2 · Path of Exile 2 · Diablo 4 · Always up to date.*

---

## 📋 Overview

Build Hub is a personal, self-hosted web app for managing and referencing endgame gaming builds. It runs as a collection of static HTML files — no backend, no database, no dependencies. Just open and play.

The app is designed for **iPad use** and served directly from a **Proxmox LXC container via Nginx**, with automatic updates through this GitHub repository.

---

## 🎮 Builds Included

### The Division 2 (Year 8, Season 1)

| Build | Tier | Playstyle | Key Items |
|---|---|---|---|
| ❤️ **Heartbreaker** | S | DPS + Survivability | Kingbreaker AR · Memento · Picaro's |
| ⚡ **St. Elmo's Engine** | S | Shock SMG · #1 Meta | St. Elmo's · Memento · Brand Chest |
| 🦎 **Chameleon** | A | High RPM Crit DPS | Chameleon AR · Memento · Brand Chest |
| ☣️ **Pestilence** | A | LMG DoT · Group DPS | Pestilence LMG · Memento · Picaro's |
| 💻 **Bluescreen** | A | Disruptor LMG · Y8S1 | Bluescreen LMG · Tipping Scales · Salvo |

### Path of Exile 2 (Patch 0.5 · Season 13)

| Build | Tier | Playstyle | Ascendancy |
|---|---|---|---|
| ☠️ **Poisonburst Pathfinder** | S | Poison DoT · Map + Boss | Pathfinder |
| 🐦‍⬛ **Spiraling Conspiracy** | A | Minion DoT · Passive Clear | Infernalist |

### Diablo 4 (Season 13 · Lord of Hatred)

| Build | Tier | Playstyle | Key Items |
|---|---|---|---|
| 💀 **Shadow Warrior Necro** | S | Minion Army · All Content | Bloodless Scream · Deathgrip · Undercrown |

---

## 📁 File Structure

```
📦 build-hub/
 ├── 📄 README.md
 ├── 📄 CHANGELOG.md
 ├── 🌐 gaming-builds-app.html      ← Main app (start here)
 ├── 🌐 guide_heartbreaker.html
 ├── 🌐 guide_stelmos.html
 ├── 🌐 guide_chameleon.html
 ├── 🌐 guide_pestilence.html
 ├── 🌐 guide_bluescreen.html
 ├── 🌐 guide_poisonburst.html
 ├── 🌐 guide_spiraling.html
 └── 🌐 guide_necromancer.html
```

> ⚠️ All files must be in the **same folder** for guide links to work correctly.

---

## 🖥️ Self-Hosting on Proxmox

```
iPad Browser  (Tailscale VPN — accessible anywhere)
    ↓
Proxmox LXC · Debian 12 · Nginx · "Redacted"
    ↓ git pull every 5 minutes (Cronjob)
GitHub Repository  ←── Claude generates updates
    ↑
You push new builds / patch updates
```

### Access

| Network | URL |
|---|---|
| Home | `Redacted` |
| Anywhere (Tailscale) | `Redacted` |

### Quick Setup Reference

```bash
# Install
apt update && apt install nginx git curl -y

# Clone repo
git clone https://github.com/KSchoene007/BuildHub.git /var/www/html/buildhub
chown -R root:root /var/www/html/buildhub
git config --global --add safe.directory /var/www/html/buildhub

# Auto-update Cronjob (every 5 min)
*/5 * * * * cd /var/www/html/buildhub && git pull origin main >> /var/log/buildhub-update.log 2>&1

# Manual update (always use this after pushing)
cd /var/www/html/buildhub && git restore . && git pull origin main
```

---

## 🔄 Update Workflow

1. Share patch notes / new info with Claude
2. Claude analyzes and generates updated HTML files
3. Download and upload to this repo
4. Commit & push
5. Server auto-pulls within 5 minutes ✅

---

## 📝 Versioning & Build Accuracy Rules

Every guide shows its version in the header. Full history in [`CHANGELOG.md`](./CHANGELOG.md).

### Division 2 Gear Rules

| Gear Type | Talent | Rule |
|---|---|---|
| **Set Gear** | Fixed — cannot change | Min. 4× pieces for set bonus |
| **Named Items** | Fixed Named Talent | Only 1 per slot type |
| **Brand Pieces** | Freely choosable | e.g. Obliterate on Chest |
| **Exotic Armor** | Fixed Exotic Talent | Max. 1 Exotic armor at a time |

### Striker Battlegear — Optimal Slot Distribution
- **4× Set:** Mask + Gloves + Holster + Kneepads
- **Backpack:** Memento (Exotic) — Kill Confirmed > Striker Backpack talent
- **Chest:** Brand Piece with Obliterate (freely choosable)

---

## 🎨 Design System

| Element | Value |
|---|---|
| Background | `#0c080e` Dark |
| Division 2 Accent | `#3a8fff` Blue |
| PoE 2 Accent | `#E8A820` Orange |
| Diablo 4 Accent | `#8B20CC` Purple |
| Fonts | Rajdhani (headers) · Exo 2 (body) |

---

## 📱 iPad Optimization

- Fully responsive (iPad Air / iPad Pro)
- Touch-friendly navigation
- Tailscale VPN — accessible from anywhere
- Home Screen Icon (Add to Home Screen in Safari)

---

*Build Hub · Personal Project · Updated with every major patch*
*The Division 2 (Y8S1) · Path of Exile 2 (S13 / Patch 0.5) · Diablo 4 (S13 Lord of Hatred)*
