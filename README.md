# 🎮 Build Hub
 
<div align="center">
![Build Hub](https://img.shields.io/badge/Build_Hub-v1.0-E03060?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyTDIgN2wxMCA1IDEwLTV6TTIgMTdsOCA0IDgtNE0yIDEybDggNCA4LTQiLz48L3N2Zz4=)
![Games](https://img.shields.io/badge/Games-2-E8A820?style=for-the-badge&logo=steam&logoColor=white)
![Builds](https://img.shields.io/badge/Builds-6-2FB8B4?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-4CAF50?style=for-the-badge)
![iPad](https://img.shields.io/badge/iPad_Ready-✓-E03060?style=for-the-badge&logo=apple&logoColor=white)
 
**A personal gaming build reference hub — optimized for iPad, self-hosted on Proxmox.**  
*The Division 2 · Path of Exile 2 · Always up to date.*
 
</div>
---
 
## 📋 Overview
 
Build Hub is a personal, self-hosted web app for managing and referencing endgame gaming builds. It runs as a collection of static HTML files — no backend, no database, no dependencies. Just open and play.
 
The app is designed for **iPad use** and served directly from a **Proxmox LXC container via Nginx**, with automatic updates through this GitHub repository.
 
---
 
## 🎮 Builds Included
 
### The Division 2
 
| Build | Tier | Playstyle | Exotic |
|---|---|---|---|
| ❤️ **Heartbreaker** | S | DPS + Survivability | Memento / Coyote's Mask |
| ⚡ **St. Elmo's Engine** | S | Shock AR · #1 Meta | Memento |
| 🦎 **Chameleon** | A | High RPM Crit DPS | Memento |
| ☣️ **Pestilence** | A | LMG DoT · Group DPS | Coyote's Mask |
 
### Path of Exile 2 (Patch 0.5)
 
| Build | Tier | Playstyle | Ascendancy |
|---|---|---|---|
| ☠️ **Poisonburst Pathfinder** | S | Poison DoT · Map + Boss | Pathfinder |
| 🐦‍⬛ **Spiraling Conspiracy** | A | Minion DoT · Passive Clear | Infernalist |
 
---
 
## 📁 File Structure
 
```
📦 build-hub/
 ├── 📄 README.md               ← You are here
 ├── 📄 CHANGELOG.md            ← Version history
 ├── 🌐 gaming-builds-app.html  ← Main app (start here)
 ├── 🌐 guide_heartbreaker.html
 ├── 🌐 guide_stelmos.html
 ├── 🌐 guide_chameleon.html
 ├── 🌐 guide_pestilence.html
 ├── 🌐 guide_poisonburst.html
 └── 🌐 guide_spiraling.html
```
 
> ⚠️ All files must be in the **same folder** for the guide links to work correctly.
 
---
 
## 🖥️ Self-Hosting on Proxmox
 
The Build Hub is served from a lightweight LXC container on Proxmox via Nginx.  
GitHub acts as the version control layer — the server auto-pulls on every new commit.
 
```
iPad Browser
    ↓
Proxmox LXC (Nginx)
    ↓  auto-pull on commit
GitHub Repository  ←──  Claude generates updates
    ↑
You push new builds / patch updates
```
 
### Quick Setup (LXC + Nginx)
 
```bash
# 1. Update & install Nginx + Git
apt update && apt install nginx git -y
 
# 2. Clone this repo into the webroot
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git /var/www/html/buildhub
 
# 3. Set permissions
chown -R www-data:www-data /var/www/html/buildhub
 
# 4. Auto-update via Cronjob (every 5 minutes)
crontab -e
# Add this line:
*/5 * * * * cd /var/www/html/buildhub && git pull origin main
```
 
Then open on iPad: `http://YOUR-SERVER-IP/buildhub/gaming-builds-app.html`
 
---
 
## 🔄 Update Workflow
 
When a new patch drops or a build changes:
 
1. **Share patch notes** with Claude in the chat
2. **Claude analyzes** what changed and generates updated HTML files
3. **Download** the new files and replace them in this repo
4. **Commit & push** — one command:
   ```bash
   git add . && git commit -m "Update: Patch X.X changes" && git push
   ```
5. **Server auto-pulls** within 5 minutes — iPad shows the new version ✅
---
 
## 📝 Versioning
 
Every guide displays its version number directly in the header (e.g. `v1.2 · Patch 0.6`).  
Full version history is tracked in [`CHANGELOG.md`](./CHANGELOG.md).
 
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
| Named Item | ⭐ Purple border |
 
---
 
## 📱 iPad Optimization
 
- Fully responsive layout (tested on iPad Air / iPad Pro)
- Touch-friendly card navigation
- No external dependencies at runtime (fonts load from Google Fonts CDN)
- Works offline after first load (browser cache)
---
 
<div align="center">
*Build Hub · Personal Project · Updated with every major patch*  
*The Division 2 (Year 8) · Path of Exile 2 (Patch 0.5+)*
 
</div>
