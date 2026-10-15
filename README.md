# jqdevAM.github.io

**The developer site, and the reason it exists separately from `pin16-site`.**

`app-ads.txt` has to sit at the *root of the host* named as the developer
website in the Play listing. GitHub Pages serves a project repository under a
path — `jqdevam.github.io/pin16-site/` — so a file put there is never the one
a crawler asks for. Only a repository named `<user>.github.io` is served at
the bare host, which is what this repository is for.

| File | What |
|---|---|
| `app-ads.txt` | The authorised sellers list for the apps, at `https://jqdevam.github.io/app-ads.txt`. |
| `ads.txt` | The same for this host's *web* inventory, of which there is none. Published because the network issues both and an account missing one half-passes its checks. |
| `google6823666341c29d91.html` | Search Console's proof that this host is ours. **Do not delete**: Google re-checks it, and Verdict's OAuth consent screen depends on the domain staying verified. |
| `index.html` | The developer page: one card per app, each linking to the app's own site and privacy policy. |
| `pin16.png`, `tintora.png`, `wobblo.png`, `verdict.png` | The app icons the cards show, copied from each app's `site/`. |

**Adding an app:** copy one `<article class="app …">` in `index.html`, give it
a class with its own `--accent` (light and dark) in the style block, and add
its icon. The app's own pages live in its own `<app>-site` repository.

## app-ads.txt

**Issued by the ad networks, not written here.** One file for every app on
this host, so it carries **both** networks the apps use, each list committed
as its network issued it:

- **Yandex** (Pin16, since 2026-10-15) — downloaded whole from the Yandex
  partner interface: the account's own `yandex.com, 106035853, DIRECT` and
  the resellers. The top of the file.
- **Start.io** (Wibblewall and Kulora) — from the Start.io portal: the
  account's own `start.io, 174889717, DIRECT` and its resellers, appended
  after a `# Start.io` comment. Lines Yandex's list already had are not
  repeated.

Everything but the two `DIRECT` account lines is a reseller the network
authorises on its behalf. **Never replace the file with one network's list**:
the other network's inventory, in another app, would become unauthorised.

Yandex re-reads the file once a day. Some demand-side platforms do not buy
impressions from an app whose developer site has no `app-ads.txt` at all, so
a stale or missing file is lost revenue rather than a paperwork failure.

**To update it:** download the network's current list from its portal and
replace that network's part only — Yandex's above the `# Start.io` comment,
Start.io's below it — then commit. Do not hand-edit records — a wrong ID here reads as
this app authorising a seller it does not use.

**The file is also committed in `pin16/site/app-ads.txt`**, byte for byte.
That repository's tests assert both `DIRECT` lines by account — which is
where "never replace it with one network's list" stops being advice and
starts failing a build. This copy is the published one and therefore the
original: `diff` the two after any change here, and copy this way round.

## ads.txt

Issued by the same Yandex account, for the same host. The pages served here
are three privacy policies and a developer page, none of which carries
advertising, so nothing listed in it can be bought. It is published anyway:
the network issues the pair, and an account with only one of them is an
account whose checks half pass. `app-ads.txt` is the file the apps are
actually verified by.

**The Play listing has to point here.** The crawler takes the developer
website from the store listing and fetches `<that host>/app-ads.txt`. If the
website field is empty or points somewhere else, the file is never read,
however correct it is.
