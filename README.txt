# FireCheck — Fire Alarm Inspection Web App

## Files
- `admin.html` — Property manager dashboard (add alarms, view logs, print QR codes)
- `inspect.html` — Tenant/inspector page (loads when a QR code is scanned)

## How to deploy

### Option A — Local network (simplest, no cost)
1. Put both files in the same folder on any computer or NAS on your network
2. Open admin.html in a browser and add your alarms
3. The QR codes will link to `inspect.html?alarm=ALARM_ID` using your local IP
   - Before printing QR codes, make sure you're viewing admin.html via its full local IP URL
     (e.g. `http://192.168.1.50/firealarm/admin.html` not just opening the file)
   - This ensures QR codes contain the correct network URL tenants can reach

### Option B — Free static hosting (recommended for real use)
Upload both files to any of these free hosts — no server needed:

**Netlify (easiest)**
1. Go to netlify.com → drag the entire folder to the deploy zone
2. Get a free URL like `https://yourname.netlify.app`
3. Open admin.html at that URL, add your alarms — QR codes will use that URL automatically

**GitHub Pages**
1. Create a repo, upload both files
2. Go to Settings → Pages → enable GitHub Pages from main branch
3. Your URL: `https://yourusername.github.io/yourrepo/admin.html`

**Cloudflare Pages**
1. Connect your GitHub repo to Cloudflare Pages
2. Free URL with HTTPS included

### Option C — Local file (testing only)
Opening the files directly from your desktop (file:// URLs) works for testing
but QR codes will contain file:// paths that won't work on other devices.

## How it works
- All data is stored in the browser's localStorage on the device running admin.html
- When a tenant scans a QR code, inspect.html reads the alarm ID from the URL,
  shows the correct instructions, and saves the sign-off back to localStorage
- Important: admin.html and inspect.html must be on the SAME domain/device for
  localStorage to be shared. This is automatically true with any of the hosting options above.

## Adding more alarms
Open admin.html → Alarms tab → fill in the form → click Add alarm.
Each alarm gets its own unique QR code. Print and stick it on or near the alarm.

## Viewing inspection records
Open admin.html → Inspection Log tab.
You can also export all records to CSV from this page.

## Notes
- Data is stored locally in the browser — clearing browser data will clear records.
  For a permanent cloud database, the app can be upgraded to use Firebase or Supabase.
- For multi-device access (e.g. property manager on desktop + tenants on phones),
  use one of the hosted options above. All scans from any device will be saved.
