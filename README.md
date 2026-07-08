# Mile Marker — Personal Running Coach

A free, self-contained marathon coach that runs entirely in your browser. One HTML file, no server, no subscription, no accounts. All data is stored locally on your device and never sent anywhere.

**File:** `mile-marker.html` (rename to `index.html` when hosting)

---

## What it does

| Page | Contents |
|---|---|
| **Home** | Race-day countdown bib, readiness score (form + sleep + HRV + resting HR), fitness/fatigue/form, this week's mileage, last night's sleep, latest runs |
| **Training** | Performance-management chart (CTL/ATL/TSB), 16-week volume with ramp-rate injury warning, long-run progression, Riegel race predictions vs. your goal |
| **Sleep** | Nightly stage breakdown (deep/core/REM/awake), 7-night sleep debt, bedtime consistency, 30-night stage averages, pace-after-good-sleep vs. short-sleep comparison |
| **Body** | HRV trend vs. your personal 30-day baseline band, resting heart rate trend, VO₂max |
| **Coach** | Detects whether your last run was easy / speed / long, queues the matching post-run stretch routine with a guided timer, and shows tips matched to your training phase (base → build → peak → taper → race week) |
| **Sync** | Strava connection, Apple Health import, profile & race settings, backups |

---

## One-time setup (~10 minutes)

### 1. Host the file (needed for Strava login)
Strava's sign-in must redirect back to a real web address, so the file needs a URL.

1. Create a free account at github.com.
2. Create a new **public** repository (any name, e.g. `run-coach`).
3. Upload `mile-marker.html` and rename it `index.html`.
4. Repo **Settings → Pages → Source: Deploy from a branch → main → Save**.
5. After a minute your app is live at `https://YOURNAME.github.io/run-coach/`.

### 2. Install on your devices
- **iPhone:** open the URL in Safari → Share → **Add to Home Screen**. It behaves like an app.
- **MacBook:** open the same URL in Safari or Chrome and bookmark it (Chrome: ⋮ → Cast/Save → Install page as app, if offered).

### 3. Connect Strava (covers Runna and Garmin runs)
1. Go to [strava.com/settings/api](https://www.strava.com/settings/api) and create an app — any name, category "Data Importer".
2. Set **Authorization Callback Domain** to your host, e.g. `YOURNAME.github.io` (no `https://`, no path). The app's Sync tab shows the exact value to use.
3. Copy the **Client ID** and **Client Secret** into the Sync tab and press **Connect Strava**.
4. In **Runna**: Settings → Integrations → connect Strava.
5. In **Garmin Connect** (if you use it): Settings → Connected Apps → Strava.

From then on, every workout flows in automatically. The app re-syncs itself each time you open it (if the last sync is more than 2 hours old), or press **Sync now**.

### 4. Import sleep & recovery data (occasional)
Apple restricts Health data to native iOS apps, so no web app can read it live. Instead:

1. iPhone Health app → your picture (top right) → **Export All Health Data**.
2. Save the zip to Files, long-press → **Uncompress**.
3. In the app's Sync tab, choose the **export.xml** inside the folder.

This imports sleep stages, HRV, resting heart rate, VO₂max, and weight. Large files are fine — it reads in chunks. The app keeps everything already imported, so a monthly top-up is plenty. Garmin watch sleep reaches Apple Health if you enable Health sync in Garmin Connect.

---

## Using it on both iPhone and MacBook
Data lives on each device separately. Two options:
- **Simplest:** connect Strava on both devices (runs sync everywhere automatically) and import the Health export on the device you use most.
- **Full copy:** Sync tab → **Export backup** on one device, **Import backup** on the other. The backup includes your Strava connection, so you only set it up once.

## Try it first
Sync tab → **Load sample data** fills the app with a realistic 16-week marathon build so you can explore every page. **Erase all data** clears it when you're ready to connect your own.

---

## How the numbers work

- **Training load** per run: Banister TRIMP from your average heart rate and your max/resting HR (set these in Profile for accuracy). Without HR, duration-based estimate.
- **Fitness (CTL)** = 42-day exponentially weighted average of daily load. **Fatigue (ATL)** = 7-day. **Form (TSB)** = fitness − fatigue. Racing feels best around −5 to +15; sustained values below −25 signal overreaching.
- **Readiness (0–100)** blends form (30%), last night's sleep vs. your goal (30%), today's HRV vs. your 30-day baseline (25%), and resting HR vs. baseline (15%). Missing signals are excluded and weights renormalized.
- **Race predictions** use the Riegel formula (exponent 1.06) from your fastest recent effort between 5K and half-marathon distance.
- **Ramp warning** flags weeks tracking more than ~10–18% above your 4-week average volume.
- **Sleep debt** = shortfall vs. your sleep goal summed over 7 nights. **Consistency** = standard deviation of bedtime over 14 nights.

## Troubleshooting

- **"Connect" bounces back with an error** — the Callback Domain in your Strava API settings must exactly match your host (e.g. `yourname.github.io`).
- **Sync fails with rate limit** — Strava allows 100 requests per 15 minutes on free API apps; wait and retry.
- **No sleep showing** — confirm the export contains sleep (a phone on the nightstand doesn't record stages; an Apple Watch or Garmin does).
- **Storage full warning** — export a backup, erase, re-import. Years of data fit comfortably, so this is rare.
- **Opening the raw file (`file://`) directly** — everything works except the Strava login, which needs the hosted URL.

## Privacy
No analytics, no server, no third parties. Your Strava tokens and all health data stay in your browser's local storage. Talk directly: your browser ↔ Strava's API, nothing in between.
