# Setup Instructions for `team-info` repo

## 1. Create the repo

Create `team-info` under **506IRRUS-4LogisticsTeam** org on GitHub (public or private — Pages works either way with a Pro/Team plan).

## 2. Push these files

```bash
cd team-info
git init
git add .
git commit -m "Initial commit — site migrated from 506IRRU-S4-Mod-Team"
git remote add origin https://github.com/506IRRUS-4LogisticsTeam/team-info.git
git branch -M main
git push -u origin main
```

## 3. Add the `PROJECT_PAT` secret

Go to **Settings → Secrets and variables → Actions → New repository secret**

- **Name:** `PROJECT_PAT`
- **Value:** Same PAT used in the old repo (needs `read:project` and `repo` scopes)

This is required for:
- The roadmap workflow to read from Projects v2 board #6
- The workflow to push commits back to this repo

## 4. Enable GitHub Pages

Go to **Settings → Pages**

- **Source:** Deploy from a branch
- **Branch:** `main` / `/ (root)`
- Click **Save**

## 5. Verify

After a minute or two, the site will be live at:

**https://506irrus-4logisticsteam.github.io/team-info/**

## What connects where

| Connection | Target | How |
|------------|--------|-----|
| Roadmap data | Org Projects v2 board #6 | GraphQL API via `PROJECT_PAT` secret |
| Workshop links | reforger.armaplatform.com | Static URLs in index.md / README.md |
| Unit website | 506thir.net | Static link in header |
| Auto-update schedule | Every 6 hours + manual dispatch | `.github/workflows/update-roadmap.yml` |

## Files in this repo

```
_config.yml                        # Jekyll config (Slate theme)
_layouts/default.html              # Custom layout — OD green styling, no repo links
index.md                           # GitHub Pages source (the live site)
README.md                          # Same content, rendered on GitHub
.github/workflows/update-roadmap.yml  # Auto-pulls roadmap from Projects v2
SETUP.md                           # This file (delete after setup)
```

## Optional: Clean up old repo

Once this repo is confirmed working, you can remove the Pages files (`index.md`, `_config.yml`, `_layouts/`, `.github/workflows/update-roadmap.yml`) from `506IRRU-S4-Mod-Team` and disable Pages there.
