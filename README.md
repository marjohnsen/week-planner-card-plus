# Week Planner Card Plus (Skylight-style)

**Week Planner Card Plus** is a fork of the excellent **Week Planner Card** by FamousWolf, with extra features aimed at a **Skylight-style family calendar dashboard**.

This “Plus” version adds UI behavior needed for our Skylight dashboard setup (for example: working **Add button** + **hash-based popup routing** fixes), and is designed to pair nicely with the companion integration:
- **ICS Calendar Tools** (edit/delete support for Local Calendar `.ics` calendars)

> If you only want the original Week Planner Card, see:  
> FamousWolf/week-planner-card

---

## What’s different in “Plus”
- ✅ Tap **any day** to open actions (Add / Edit / Delete)
- ✅ **Add / Edit / Delete** event flows built into the UI (Skylight-style)
- ✅ Fixes for the **Add button** behavior (restored + reliable)
- ✅ Fixes for **hash / popup routing** used in our Skylight-style dashboard
- ✅ Designed to pair with **ICS Calendar Tools** so edits/deletes persist to **Local Calendar (.ics)** https://github.com/randrcomputers/ics-calendar-tools

---
<img width="1903" height="961" alt="image" src="https://github.com/user-attachments/assets/beef1e76-9105-4a71-8ef1-2d6ef66e6c6a" />

## Installation

### HACS (Recommended)
1. Make sure HACS is installed and working.
2. Go to **HACS → Frontend**.
3. Open the menu (top right) → **Custom repositories**.
4. Add this repo URL:
   - `https://github.com/randrcomputers/week-planner-card-plus`
5. Category: **Lovelace**
6. Install **Week Planner Card Plus**.
7. Restart Home Assistant (or reload resources if you prefer).

#### Add the Lovelace Resource
HACS usually offers to add the resource automatically, but you can do it manually IF NEEDED ONLY:

**Settings → Dashboards → Resources → Add Resource**
- URL (typical HACS path):
  - `/hacsfiles/week-planner-card-plus/week-planner-card-plus.js`
- Type:
  - `JavaScript Module`

> If your built file name/path differs, use the file that exists in your installed `/config/www/community/` folder.

---

### Manual Install (advanced)
1. Copy the built `.js` file into:
   - `/config/www/`
   (or `/config/www/community/week-planner-card-plus/`)
2. Add a Resource:

Example:
- URL:
  - `/local/week-planner-card-plus.js`
- Type:
  - `JavaScript Module`

---

## Basic Usage

Add a card to a dashboard:

```yaml
type: custom:week-planner-card-plus
calendars:
  - entity: calendar.family_calendar
days: 7
