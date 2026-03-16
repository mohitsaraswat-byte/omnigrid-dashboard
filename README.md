# OMNIGRID Team Dashboard

Live team efficiency dashboard — works with Google Sheets CSV, no backend needed.

## What it does

- **2024** — embedded data, loads instantly (offline capable)
- **2025 Live** — fetches directly from your published Google Sheet on page load
- Automatic background fetch on open, toggle between years with one click
- All 6 pages: Overview, Team Performance, Subject View, Trends, Attendance, Members
- Every member has a full profile: monthly charts, weekly charts, attendance pie, radar vs team avg

---

## Setup (5 minutes)

### Step 1 — Publish your Google Sheet as CSV

1. Open your Google Sheet
2. Go to **File → Share → Publish to web**
3. First dropdown → select the **"Team View - Efficiency Tracker"** tab
4. Second dropdown → select **CSV**
5. Click **Publish** → confirm → copy the URL

It looks like:
```
https://docs.google.com/spreadsheets/d/e/2PACX-.../pub?output=csv
```

### Step 2 — The CSV URL is already set

The dashboard already has your URL configured:
```js
const CSV_2025 = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTXll3...pub?output=csv';
```

If it ever changes, update that one line.

### Step 3 — Add to your OMNIGRID GitHub repo

```bash
# Copy to your repo
cp OMNIGRID_Dashboard.html /path/to/omnigrid-repo/dashboard.html

# Commit and push
cd /path/to/omnigrid-repo
git add dashboard.html
git commit -m "feat: add live team efficiency dashboard"
git push
```

### Step 4 — Enable GitHub Pages

1. Go to your GitHub repo → **Settings → Pages**
2. Source: **Deploy from a branch** → branch: **main** → folder: **/ (root)**
3. Save

Live URL:
```
https://YOUR_USERNAME.github.io/YOUR_REPO/dashboard.html
```

---

## Using Vercel instead (already set up for OMNIGRID)

```bash
cp OMNIGRID_Dashboard.html public/dashboard.html
```

Live at: `https://your-project.vercel.app/dashboard.html` on next deploy.

---

## Column requirements

The sheet must have these columns (your current setup already matches):

| Column | Expected keyword |
|--------|-----------------|
| Employee name | `Faculty name` |
| Date | `Date of Work` |
| Attendance | `Attendence` |
| Week number | `Week number` |
| Productivity % | `Overall Productivity (%)` |
| Hours worked | `Overall hours worked` |

---

## Adding new members to subject mapping

New members auto-appear in the dashboard. If they show as "Other" subject, add them to `SUBJECT_MAP` in the HTML:

```js
const SUBJECT_MAP = {
  // existing entries...
  'new member name lowercase': 'Physics',
};
```

---

## How live data works

- Dashboard opens → fetches CSV in background (takes ~1-2 seconds)
- "2025 Live" button activates once data is ready
- Page reload = fresh data
- No API key, no login, no server needed
