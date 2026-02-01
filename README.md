# Week Planner Card Plus (Skylight-style)

**Week Planner Card Plus** is a fork of the excellent **Week Planner Card** by FamousWolf, with extra features aimed at a **Skylight-style family calendar dashboard**.  
This “Plus” version adds UI behavior needed for our Skylight dashboard setup (for example: a working **Add button** + **hash-based popup routing** fixes), and it can be used with both **cloud calendars** (Google / CalDAV / etc.) and **Local Calendar (.ics)**.  

For Local Calendar `.ics` add/edit/delete support, it’s designed to pair nicely with the companion integration:
- **ICS Calendar Tools** (add/edit/delete + repeat support for Local Calendar `.ics` calendars)  
  https://github.com/randrcomputers/ics-calendar-tools

> If you only want the original Week Planner Card, see:  
> FamousWolf/week-planner-card

---

## What’s different in “Plus”
- ✅ Tap **any day** to open actions (Add / Edit / Delete)
- ✅ **Skylight-style** UI flows (popup routing / interaction behavior)
- ✅ Fixes for the **Add button** behavior (restored + reliable)
- ✅ Fixes for **hash / popup routing** used in our Skylight-style dashboard
- ✅ Optional pairing with **ICS Calendar Tools** so edits/deletes persist to **Local Calendar (.ics)**  
  https://github.com/randrcomputers/ics-calendar-tools

---

## Calendar support (Google / cloud + Local Calendar)

Week Planner Card Plus works with **Home Assistant calendar entities** (`calendar.*`) from many sources.  
**What you can do (Add/Edit/Delete/Repeat) depends on what your calendar integration supports.**

### Cloud calendars (Google / CalDAV / etc.)
- ✅ **View events** in the planner
- ✅ **Add events**
- ✅ **Delete events**
- ✅ **Repeat** supported
- ⚠️ **Edit support varies** by provider/integration and configuration

### Local Calendar (.ics)
- ✅ **View events**
- ✅ **Add events**
- ✅ **Edit/Delete** typically requires **ICS Calendar Tools** to modify the underlying `.ics` file
- ✅ **Repeat (RRULE)** supported via ICS Calendar Tools

---

<img width="1903" height="961" alt="image" src="https://github.com/user-attachments/assets/beef1e76-9105-4a71-8ef1-2d6ef66e6c6a" />
<img width="1914" height="963" alt="image" src="https://github.com/user-attachments/assets/cf921957-3e9f-4736-ad09-dd473233b4a7" />

---

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

## IMPORTANT: Browser cache / `.js.gz`
If you update the `.js` but nothing changes, Home Assistant / your browser may still be serving a compressed copy.

If you see a file like this in the same folder:
- `week-planner-card-plus.js.gz`

Delete it, then hard refresh your browser:
- **Ctrl+F5** (Windows)
- **Cmd+Shift+R** (Mac)

This prevents “I updated it but it’s still old” headaches.

---

## Basic Usage

Add a card to a dashboard:

```yaml
Old popup(scripted)
type: custom:week-planner-card-plus
tapEmptyDayToAdd: true # This is old legacy popup
clickEmptyDayToAddPlus: false # this is the new built in UI popup with recurring events support!
calendars:
  - entity: calendar.family_calendar

New popup with recurring support!

type: custom:week-planner-card-plus
tapEmptyDayToAdd: false # This is old legacy popup
clickEmptyDayToAddPlus: true # this is the new built in UI popup with recurring events support!
calendars:
  - entity: calendar.family_calendar

```
