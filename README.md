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
| `yandex_708eb66831f3c345.html` | Yandex Webmaster's proof that this host is ours. **Do not delete**: Yandex re-checks it. |
| `robots.txt` | Lets crawlers in and names each app's sitemap. Crawlers read it only at the host root, which is why it lives here and not in an app's site. Pin16's sitemap lists its fault-code pages; add a `Sitemap:` line when another app publishes one. The Yandex group's `Clean-param` folds the code search's `?q=` addresses into the one page they are. |
| `index.html` | The developer page: one card per app, each linking to the app's own site and privacy policy. |
| `pin16.png`, `tintora.png`, `wobblo.png`, `verdict.png` | The app icons the cards show, copied from each app's `site/`. |

**Adding an app:** copy one `<article class="app …">` in `index.html`, give it
a class with its own `--accent` (light and dark) in the style block, and add
its icon. The app's own pages live in its own `<app>-site` repository.

## The repositories

**Nine, and the split is deliberate.** Four app repositories, private,
where the code and the docs live; a public mirror for each, holding only the
pages the public is meant to reach; and this one, which is the host itself.

| Repository | Public | What it holds |
|---|---|---|
| `pin16` | no | **Pin16** — OBD-II diagnostics, Flutter, `com.amaldavanau.pin16` |
| `tintora` | no | **Kulora** — the colour app, Flutter |
| `wobblo` | no | **Wibblewall** — the live wallpaper, Android/Kotlin |
| `verdict` | no | **Verdict** — the Play review-state watcher, Android/Kotlin |
| `pin16-site`, `tintora-site`, `wobblo-site`, `verdict-site` | yes | A copy of that app's `site/`: the page about the app, and the privacy policy its listing links to |
| `jqdevAM.github.io` | yes | This: the sellers files, Search Console's proof, and the developer page all four listings name |

The four apps are one body of work by one developer, and a decision taken in
one — the ad network, the consent question, a sentence of policy, a default
in a build script — is nearly always the same decision in the others.

**A mirror is a second push, and nothing fails when it is skipped.** The
policy is written and reviewed in the app repository; the copy in the
`-site` repository is the only one anybody reads. On 16 October 2026 three
of the four were behind the policies they publish:

- **Kulora's** still named Start.io as the network serving both banners, a
  day after the app moved back to Yandex;
- **Wibblewall's** still named Start.io too, and still said the app asks for
  nothing needing your approval — on the day it began asking for permission
  to notify;
- **Pin16's** was three weeks old: it named the right network, but not the
  three permissions its SDK declares, nor the unused Start.io SDK that is
  still in the build.

Nothing in Play Console, in either app, or in any build says a word about
it. `diff` between the two copies is the only check there is.

## app-ads.txt

**Issued by the ad networks, not written here.** One file for every app on
this host, so it carries **both** networks the apps use, each list committed
as its network issued it:

- **Yandex** (all three apps, since 2026-10-15) — downloaded whole from the
  Yandex partner interface: the account's own
  `yandex.com, 106035853, DIRECT` and the resellers. The top of the file.
- **Start.io** (no app, since 2026-10-15) — from the Start.io portal: the
  account's own `start.io, 174889717, DIRECT` and its resellers, appended
  after a `# Start.io` comment. Lines Yandex's list already had are not
  repeated. **Kept although nothing is served by it**: a banner is one
  `slots.` line from going back, and a list removed is a list to be asked
  for again.

Everything but the two `DIRECT` account lines is a reseller the network
authorises on its behalf. **Never replace the file with one network's
list.** It cost nothing on 15 October, when the last app moved to Yandex and
Start.io's half became dead weight rather than load-bearing; it costs an
app's revenue on the day one banner goes back, and nothing in any app or
console says that it has.

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
