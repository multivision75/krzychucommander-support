# Krzychu Commander — support & marketing site

Static site for GitHub Pages. Used for the App Store Connect listing fields:

| Field | URL |
|---|---|
| Support URL | <https://multivision75.github.io/krzychucommander-support/> |
| Marketing URL | <https://multivision75.github.io/krzychucommander-support/> |
| Privacy Policy URL | <https://multivision75.github.io/krzychucommander-support/privacy.html> |

The URLs assume a `krzychucommander-support` repository with GitHub Pages enabled (branch
`main`, root folder); `docs/site/` here is the source of truth, the support repo only its mirror.

## Contents

- `index.html` — app description, features, screenshots, keys, support contact, FAQ
- `privacy.html` — privacy policy, English and Polish
- `assets/` — app icon (from the built `appicon.icns`) and screenshots (the Help's dark ones from `Resources/Raw/Help/`)
- `.nojekyll` — tells GitHub Pages to serve the files as-is

`privacy.html` and `docs/privacy-policy.md` are two copies of the same policy, so a change of
wording has to be made in both. Update the policy when the app starts contacting a new online
service or storing new data.

Plain HTML with inline CSS, no build step. Every link and image path is relative, so the site
works from any directory, at any URL prefix, and over `file://`.

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# http://localhost:8000/
```

## Publish

```bash
KrzychuCommander/scripts/support-site.sh      # show the changes, ask, commit + push
KrzychuCommander/scripts/support-site.sh -n   # full diff only, publish nothing
```

The script clones the support repo into a temporary folder, copies `docs/site/` over it with
`--delete`, commits, pushes through `gh` (`gh auth login`) and waits for the GitHub Pages build.
Don't edit the support repo directly — the next publish overwrites it.
