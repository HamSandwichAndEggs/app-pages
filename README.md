# App pages — Sports Table Soccer Coach

The support and privacy pages App Store Connect requires, for every app published under
**sportstablesoccercoach.com**. Nothing else lives here; the apps' own source is in separate,
private repositories.

Served at **https://apps.sportstablesoccercoach.com/**

## Why this repo exists

Apple will not accept a listing without a **Support URL** and a **Privacy Policy URL**, one pair
per app, and **the privacy URL has to keep resolving for as long as the app is listed** — not just
at review. The main site is on a free website-builder plan that serves a single scrolling page and
cannot host extra paths, so the pages live here instead.

## Layout

```
/                                 index.html      lists the apps
/soccer-tactical-coach/support/                   ← Support URL
/soccer-tactical-coach/privacy/                   ← Privacy Policy URL
CNAME                             the custom domain, one hostname
.nojekyll                         stops Pages reinterpreting anything
```

**One folder per app, with `support/` and `privacy/` inside it.** Apple wants two URLs per app, so
each app gets its own pair — a shared privacy policy only works if every app makes the same claims,
and they will not. The tactics board makes no network connection at all; an app that links out to a
shop, or exports a file, cannot honestly say the same.

### Adding an app

1. Copy `soccer-tactical-coach/` to a new folder named after the app.
2. Edit the two pages: the app name, and whatever the policy actually has to say about *that* app.
3. Add a block to `index.html` — the comment there says which three things to change.
4. Push. The URLs are live in a minute or two.

The new app's URLs are then
`https://apps.sportstablesoccercoach.com/<folder>/support/` and `.../privacy/`.

## The custom domain

`CNAME` contains a single hostname, `apps.sportstablesoccercoach.com`. **GitHub Pages allows one
custom domain per repository**, which is why every app shares one subdomain and is separated by
path rather than getting a subdomain each.

To make it live, add this record wherever the domain's DNS is managed — GoDaddy, for this domain.
DNS records come with the domain registration rather than the website plan, so a free site does not
block it:

| Type | Name | Value |
|---|---|---|
| CNAME | `apps` | `hamsandwichandeggs.github.io` |

Then Settings → Pages → Custom domain, enter the hostname, and tick **Enforce HTTPS** once the
certificate is issued (it can take a few minutes).

**Why a custom domain rather than the `github.io` address.** The privacy URL goes into an App Store
listing and has to keep working for the life of the app. On `hamsandwichandeggs.github.io` that ties
the listing to GitHub permanently; on `apps.sportstablesoccercoach.com` the host can be changed
whenever you like by repointing one DNS record, and the listing never has to be touched. Changing a
URL on a live listing means a metadata update and another review pass.

## Publishing

Settings → Pages → Source: **Deploy from a branch**, branch `main`, folder `/` (root).

Without the custom domain the same pages are at
`https://hamsandwichandeggs.github.io/app-pages/soccer-tactical-coach/privacy/`. That works, and is
a reasonable way to check everything before the DNS is in place — but set the domain up before
pasting anything into App Store Connect.

**Open every URL in a private window before submitting it.** A support URL that 404s comes back as
a metadata rejection days later, not as a build failure.

## Editing

Each page is a **single self-contained file**. No stylesheet, font, script, image or analytics is
fetched from anywhere — deliberately, so a page cannot break because something else moved, and
because a privacy policy that phones out to a font CDN in order to say nothing is tracked is not
telling the truth. Keep it that way.

The tactics board's privacy wording is mirrored in `PRIVACY.md` in that app's repository.
**Change both together**, and update the "Last updated" date when the policy changes rather than
when the markup does.

## What the tactics board's pages claim

That the app collects nothing, has no accounts, no analytics and **no network use at all**. That is
true as it stands, and it is the strongest thing the policy says. Anything added later that reaches
the internet — even a link out to a shop — means the wording has to be qualified first. Do not add
the feature and fix the page afterwards.

## What the scoreboard's pages claim

That the app collects nothing, has no accounts, no analytics and no network use. Unlike the
tactics board it **exports files** (CSV and a PDF result sheet) and prints, so its policy says
those leave the device only when the user sends them, to wherever they choose. The wording is
mirrored in `PRIVACY.md` in the scoreboard's repository; change both together.
