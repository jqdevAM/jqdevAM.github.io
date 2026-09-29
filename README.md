# jqdevAM.github.io

**The developer site, and the reason it exists separately from `pin16-site`.**

`app-ads.txt` has to sit at the *root of the host* named as the developer
website in the Play listing. GitHub Pages serves a project repository under a
path — `jqdevam.github.io/pin16-site/` — so a file put there is never the one
a crawler asks for. Only a repository named `<user>.github.io` is served at
the bare host, which is what this repository is for.

| File | What |
|---|---|
| `app-ads.txt` | The authorised sellers list, at `https://jqdevam.github.io/app-ads.txt`. |
| `index.html` | The developer page: one card per app, each linking to the app's own site and privacy policy. |
| `pin16.png`, `tintora.png` | The app icons the cards show, copied from each app's `site/`. |

**Adding an app:** copy one `<article class="app …">` in `index.html`, give it
a class with its own `--accent` (light and dark) in the style block, and add
its icon. The app's own pages live in its own `<app>-site` repository.

## app-ads.txt

**Issued by the ad network, not written here.** It is downloaded whole from
the Yandex partner interface and committed unchanged. The one record that is
this account's own is `yandex.com, <partner id>, DIRECT`; everything else is
a reseller the network authorises on its behalf.

Yandex re-reads the file once a day. Some demand-side platforms do not buy
impressions from an app whose developer site has no `app-ads.txt` at all, so
a stale or missing file is lost revenue rather than a paperwork failure.

**To update it:** download the current list from the partner interface,
replace the file, commit. Do not hand-edit records — a wrong ID here reads as
this app authorising a seller it does not use.

**The Play listing has to point here.** The crawler takes the developer
website from the store listing and fetches `<that host>/app-ads.txt`. If the
website field is empty or points somewhere else, the file is never read,
however correct it is.
