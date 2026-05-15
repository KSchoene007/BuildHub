# 🎮 Build Hub

![Build Hub](https://img.shields.io/badge/Build_Hub-v1.3-E03060?style=for-the-badge)
![Games](https://img.shields.io/badge/Games-2-E8A820?style=for-the-badge&logo=steam&logoColor=white)
![Builds](https://img.shields.io/badge/Builds-7-2FB8B4?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-4CAF50?style=for-the-badge)
![iPad](https://img.shields.io/badge/iPad_Ready-%E2%9C%93-E03060?style=for-the-badge&logo=apple&logoColor=white)
![Self-Hosted](https://img.shields.io/badge/Self--Hosted-Proxmox-E8A820?style=for-the-badge)

> **A personal gaming build reference hub — optimized for iPad, self-hosted on Proxmox.**
> *The Division 2 · Path of Exile 2 · Always up to date.*

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
| ⚡ **St. Elmo's Engine** | S | Shock SMG · #1 Meta | St. Elmo's · Memento · Picaro's |
| 🦎 **Chameleon** | A | High RPM Crit DPS | Chameleon AR · Memento · Picaro's |
| ☣️ **Pestilence** | A | LMG DoT · Group DPS | Pestilence LMG · Coyote's Mask |
| 💻 **Bluescreen** | A | Disruptor LMG · Y8S1 | Bluescreen LMG · Tipping Scales · Salvo |

### Path of Exile 2 (Patch 0.5)

| Build | Tier | Playstyle | Ascendancy |
|---|---|---|---|
| ☠️ **Poisonburst Pathfinder** | S | Poison DoT · Map + Boss | Pathfinder |
| 🐦‍⬛ **Spiraling Conspiracy** | A | Minion DoT · Passive Clear | Infernalist |

---

## 📁 File Structure

```
📦 build-hub/
 ├── 📄 README.md
 ├── 📄 CHANGELOG.md
 ├── 🌐 gaming-builds-app.html   ← Main app (start here)
 ├── 🌐 guide_heartbreaker.html
 ├── 🌐 guide_stelmos.html
 ├── 🌐 guide_chameleon.html
 ├── 🌐 guide_pestilence.html
 ├── 🌐 guide_bluescreen.html
 ├── 🌐 guide_poisonburst.html
 └── 🌐 guide_spiraling.html
```

> ⚠️ All files must be in the **same folder** for guide links to work correctly.

---

## 🖥️ Self-Hosting on Proxmox

The Build Hub runs on a lightweight **Debian 12 LXC Container** on Proxmox via Nginx.
GitHub acts as the version control layer — the server auto-pulls every 5 minutes.

```
iPad Browser  (Tailscale VPN — accessible anywhere)
    ↓
Proxmox LXC · Debian 12 · Nginx · 192.168.0.190
    ↓  git pull every 5 minutes (Cronjob)
GitHub Repository  ←── Claude generates updates
    ↑
You push new builds / patch updates
```

### Access

| Network | URL |
|---|---|
| Home | `http://192.168.0.190/buildhub/gaming-builds-app.html` |
| Anywhere (Tailscale) | `http://100.113.7.28/buildhub/gaming-builds-app.html` |

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

# Manual update
cd /var/www/html/buildhub && git restore . && git pull origin main
```

---

## 🔄 Update Workflow

When a new patch drops or a build changes:

1. **Share patch notes** with Claude in the chat
2. **Claude analyzes** what changed and generates updated HTML files
3. **Download** the new files and upload to this repo
4. **Commit & push** — GitHub notifies the server
5. **Server auto-pulls** within 5 minutes ✅

> 💡 **Tip:** Always use `git restore . && git pull` on the server after pushing — this avoids merge conflicts from local fixes.

---

## 📝 Versioning

Every guide displays its version in the header (e.g. `v1.3 · Y8S1`).
Full version history in [`CHANGELOG.md`](./CHANGELOG.md).

### Build Accuracy Guidelines

| Gear Type | Talent | Rule |
|---|---|---|
| **Set Gear** | Fixed — cannot change | Never assign custom talents |
| **Named Items** | Fixed Named Talent | One specific talent, always active |
| **Brand Pieces** | Freely choosable | Pick best talent (e.g. Perfect Obliterate) |
| **Exotic Armor** | Fixed Exotic Talent | Only 1 Exotic armor piece at a time |

---

## 🎨 Design System

| Element | Value |
|---|---|
| Background | `#0c080e` Dark |
| Accent Red | `#E03060` |
| Accent Gold | `#E8A820` |
| Accent Teal | `#2FB8B4` |
| Fonts | Rajdhani (headers) · Exo 2 (body) |
| Tier S | 🥇 Gold badge |
| Tier A | 🔵 Blue badge |
| Exotic | 💎 Gold border |
| Named Item | ⭐ Gold border |
| Set Piece | 🔴 Red border |
| Brand Piece | 🩵 Teal border |

---

## 📱 iPad Optimization

- Fully responsive layout (iPad Air / iPad Pro)
- Touch-friendly card navigation
- Accessible via Tailscale VPN from anywhere
- Home Screen Icon support (Add to Home Screen in Safari)
- Works offline after first load (browser cache)

---

*Build Hub · Personal Project · Updated with every major patch*
*The Division 2 (Year 8, Season 1) · Path of Exile 2 (Patch 0.5+)*
