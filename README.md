# Ivan Music — update channel

This repo is the **public** side of IVAN MUSIC. It carries exactly three things:

## 1. Release assets (the update channel)

The app polls two FIXED urls:

- manifest: https://github.com/IvanXxxxyyuffff/ivan-music/releases/latest/download/update.json
- package : https://github.com/IvanXxxxyyuffff/ivan-music/releases/latest/download/ivan-music.apk

Asset names repeat every release on purpose -- that is what makes
`releases/latest/download/<name>` resolve. Version lives in the tag.

**This repo must stay public.** Release assets of a private repo cannot be
fetched anonymously, and the app has no token -- it would just get a 403.

## 2. Mirrors (wall-inside China)

The GitHub address above is often unreachable from mainland China -- not broken,
just throttled. The app therefore also tries reverse proxies, each of which
just prefixes the SAME GitHub url (so the bytes and the freshness rules are
identical, only the route differs):

| mirror | measured (2026-10-15) | role |
|---|---|---|
| `gh-proxy.com` | 2450 KB/s | primary |
| `gh-proxy.cc` | 970 | primary |
| `ghproxy.icu` | 270 | primary |
| `ghproxy.xyz` | 180 | primary |
| `hk.gh-proxy.com` | 120 | fallback |
| `ghfast.top` | 280 | fallback |
| `ghproxy.net` | 30 | fallback, small segments only |

Mirrors are **not** a copy of the release -- they proxy the same one. Publishing
never needs to touch them.

## 3. `tune.json` (cloud tuning)

https://raw.githubusercontent.com/IvanXxxxyyuffff/ivan-music/main/tune.json

The app fetches this at startup and applies it. Editing this file changes
behaviour **without shipping a new APK** -- e.g. adding or reordering music
source routes, cover size, per-backend quota.

- `rev` must increase. A `rev` that is not newer than the one already applied
  is ignored (so a stale CDN copy can never roll the app back).
- The file is fetched through the same mirror set as above.
- Note: `raw.githubusercontent.com` itself has a CDN cache, and in mainland
  China it often times out -- mirrors are usually *fresher* than direct raw.

**Nothing else belongs in this repo.** It is a public repo: no credentials, no
user data, no source code. Source lives in the private `ivan-music-private`.
