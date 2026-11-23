# Comeback Run Log (PWA)

An installable, offline web app version of the tracker. Your runs are stored **only on your phone**
(IndexedDB, mirrored to localStorage). Nothing is sent to a server.

## Files
| File | Purpose |
|---|---|
| `index.html` | The whole app (plan, views, storage, backup) |
| `manifest.webmanifest` | Name, colours, icons, so the phone can install it |
| `sw.js` | Service worker: caches the app so it opens offline, and handles updates |
| `icons/` | App icons (Android, maskable, iPhone, favicon) |

## 1. Host it once (HTTPS required)
A PWA has to be served over HTTPS. Pick one option:

**GitHub Pages (free, permanent)**
1. Create a GitHub repo, e.g. `run-log`. A free account needs it to be public. Only the app code goes in it, never your runs.
2. Upload every file in this folder, keeping `icons/` as a folder.
3. Repo **Settings → Pages → Deploy from a branch → `main` / root**.
4. After about a minute it is live at `https://<your-username>.github.io/run-log/`.

**Netlify (drag and drop)**
1. Sign in at app.netlify.com, then **Add new site → Deploy manually**.
2. Drag this whole folder onto the page. You get an `https://<name>.netlify.app` link.

## 2. Install on your phone
- **Android (Chrome):** open the link, then **Progress → Install app**. Or use the ⋮ menu and choose **Install app** / **Add to Home screen**.
- **iPhone (Safari):** open the link, tap **Share**, then **Add to Home Screen**.

Open it once while online. After that it works offline.

## 3. Back up
Go to **Progress → Export backup** every week or so, and always before you change phones,
uninstall, or clear browser data. **Import backup** merges a file back in. Runs that are already there are kept.
The Today tab reminds you if your last backup is more than 7 days old.

## 4. Ship an update
1. Edit the files.
2. In `sw.js`, bump `VERSION` (e.g. `'v1'` → `'v2'`). **If you skip this, phones keep the old copy.**
3. Upload the changed files to the same host.
4. Next time you open the app online, a **"A new version is ready"** bar appears. Tap **Reload**.
   Your logged runs are not affected.

## Test locally (optional)
```powershell
python -m http.server 8765 --directory "$env:USERPROFILE\Desktop\ComebackRunLog"
```
Then open http://localhost:8765 in Chrome or Edge.
