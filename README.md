# Week Planner Card Plus

v2.0.4 Added option for defaultAllDay: true|false
v2.0.3 Added support for Dutch language

**Week Planner Card Plus** is a fork of the excellent **Week Planner Card** by FamousWolf, with extra features aimed at a **Skylight-style family calendar dashboard**.  
This “Plus” version adds UI behavior needed for our Skylight dashboard setup (for example: a working **Add button** + **hash-based popup routing** fixes), and it can be used with both **cloud calendars** (Google / CalDAV / etc.) and **Local Calendar (.ics)**.

For Local Calendar `.ics` add/edit/delete support, it’s designed to pair nicely with the companion integration:

- **ICS Calendar Tools** (add/edit/delete + repeat support for Local Calendar `.ics` calendars)  
  https://github.com/randrcomputers/ics-calendar-tools

> If you only want the original Week Planner Card, see:  
> https://github.com/FamousWolf/week-planner-card

---

## What’s different in “Plus”

- ✅ **Skylight-style** UI flows (popup routing / interaction behavior)
- ✅ Fixes for the **Add button** behavior (restored + reliable)
- ✅ Fixes for **hash / popup routing** used in our Skylight-style dashboard
- ✅ **Empty-day + empty-space click-to-add** (optional, built-in dialog)
- ✅ **Edit remembers calendar** (Edit dialog preselects the clicked event’s calendar)
- ✅ **Schedule view (Skylight timeline)** + recommended CSS for all-day wrapping
- ✅ Optional pairing with **ICS Calendar Tools** so edits/deletes persist to **Local Calendar (.ics)**  
  https://github.com/randrcomputers/ics-calendar-tools

---

## Calendar support (Google / cloud + Local Calendar)

Week Planner Card Plus works with **Home Assistant calendar entities** (`calendar.*`) from many sources.  
**What you can do (Add/Edit/Delete/Repeat) depends on what your calendar integration supports.**

Note certain calendars have limitations.
CalDAV cannot edit or delete events. But you can add events
Google cannot edit events. But You can add and delete events
Local calendars you can delete, add and edit events with ics calendar tools addon!

### Cloud calendars (Google / CalDAV / etc.)
- ✅ **View events** in the planner
- ✅ **Add events** (built-in dialog)
- ✅ **Delete events**
- ✅ **Repeat** supported (built-in dialog)
- ⚠️ **Edit support varies** by provider/integration and configuration

### Local Calendar (.ics)
- ✅ **View events**
- ✅ **Add events**
- ✅ **Edit/Delete** typically requires **ICS Calendar Tools** to modify the underlying `.ics` file
- ✅ **Repeat (RRULE)** supported via **ICS Calendar Tools**

---

<img width="1903" height="961" alt="image" src="https://github.com/user-attachments/assets/beef1e76-9105-4a71-8ef1-2d6ef66e6c6a" />
<img width="1914" height="963" alt="image" src="https://github.com/user-attachments/assets/cf921957-3e9f-4736-ad09-dd473233b4a7" />
<img width="1907" height="1071" alt="image" src="https://github.com/user-attachments/assets/758644fa-1e02-468d-a77a-455502439e10" />

---

## Installation

### HACS (Recommended)

1. Make sure HACS is installed and working.
2. HACS → ⋮ → Custom repositories
3. Open the menu (top right) → **Custom repositories**.
4. Add this repo URL:
   - `https://github.com/randrcomputers/week-planner-card-plus`
5. Category: Dashboard
6. Install **Week Planner Card Plus**.
7. Restart Home Assistant (or reload resources if you prefer).

#### Add the Lovelace Resource

HACS usually offers to add the resource automatically, but you can do it manually if needed:

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

### New built-in Add dialog (recommended)

This uses the Plus card’s built-in Add dialog:
- Clicking a totally empty day opens **Add**
- Clicking empty space within a day that already has events opens **Add**
- Clicking an event opens **Edit** (and the calendar is preselected based on the clicked event)

```yaml
type: custom:week-planner-card-plus
tapEmptyDayToAdd: false           # legacy scripted popup (leave off)
clickEmptyDayToAddPlus: true      # NEW built-in dialog
calendars:
  - entity: calendar.family_calendar
```

### Legacy scripted Add dialog (older dashboards)

This uses the old “scripted” Add flow (kept for backwards compatibility).

```yaml
type: custom:week-planner-card-plus
tapEmptyDayToAdd: true            # legacy scripted popup
clickEmptyDayToAddPlus: false     # disable built-in dialog
calendars:
  - entity: calendar.family_calendar
```

> Tip: Use **only one** add mode. Set **either** `tapEmptyDayToAdd` **or** `clickEmptyDayToAddPlus` to `true` — not both.

---

## Schedule View (Skylight)

Week Planner Card Plus also includes a **Schedule** view intended to feel like a Skylight-style weekly timeline.

### Notes / Known quirks
- All-day events are rendered as **pills** at the top of each day column.
- Timed events render inside the hour grid.
- If your dashboard uses narrow columns (or long descriptions), all-day pills may visually **bleed into the next day** unless wrapping is forced via CSS.

### Required card_mod for Schedule View

```yaml
            card:
              type: custom:week-planner-card-plus
              viewMode: ${ VIEWMODE } # Needed for new scheduled view
              tapEmptyDayToAdd: false
              clickEmptyDayToAddPlus: true
              calendars:
                - entity: calendar.family_calendar
```

### Recommended card_mod CSS for Schedule View

✅ **ADD THIS: All-day pills wrap inside the day column (no bleed to next day)**

```yaml
card_mod:
  style: |
    /* ✅ ADD THIS: All-day pills wrap inside the day column (no bleed to next day) */
    .timelineAllDayPill,
    .timelineAllDayPill * {
      white-space: normal !important;
      overflow-wrap: anywhere !important;
      word-break: break-word !important;
    }
```

### Optional: force schedule text to black (Skylight readability)

If your schedule pills show white text and you want consistent dark text:

```yaml
card_mod:
  style: |
    /* Schedule view: force black text on all-day + timed pills */
    .timelineAllDayPill,
    .timelineAllDayPill * {
      color: #111 !important;
    }

    .timelineEvent,
    .timelineEvent * {
      color: #111 !important;
    }

    /* Slightly dimmer time text */
    .timelineEvent .time,
    .timelineAllDayPill .time {
      color: rgba(0,0,0,0.70) !important;
    }
```

---

## Notes on Repeat (Recurring Events)

- **Cloud calendars (Google/CalDAV/etc.)**: recurring events are created using Home Assistant’s calendar APIs (built-in dialog).
- **Local Calendar (.ics)**: recurring events require writing an RRULE into the `.ics` file — use **ICS Calendar Tools** for add/update/delete with repeat support.

---

## Options
### `defaultAllDay` (boolean)
Default state of the **All day** toggle in the built-in Add/Edit dialog.

- `true` = All day starts ON
- `false` = All day starts OFF

**Default:** `false`

### `clickEmptyDayToAddPlus` (boolean)
When `true`, empty-day / empty-space clicks open the **built-in Add dialog** (recommended).

### `tapEmptyDayToAdd` (boolean)
Legacy mode. When `true`, empty-day clicks use the **older scripted Add flow**.

---

## Companion integration (Local Calendar editing)

If you want Local Calendar `.ics` **edit/delete/repeat** to behave like cloud calendars, install:

- **ICS Calendar Tools**  
  https://github.com/randrcomputers/ics-calendar-tools
