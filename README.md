# Soccer Tactical Coach — support and privacy pages

The two web pages App Store Connect requires for the **Soccer Tactical Coach** iOS app.
Nothing else. The app's own source is in a separate, private repository.

| Path | Serves | Required by Apple as |
|---|---|---|
| `support/index.html` | `/support/` | the app's **Support URL** |
| `privacy/index.html` | `/privacy/` | the app's **Privacy Policy URL** |

## Why this repo exists

Apple will not accept a listing without both URLs, and **the privacy URL has to keep resolving for
as long as the app is listed** — not just at review. The app's own website is on a free
website-builder plan that serves a single scrolling page and cannot host extra paths, so these
live here instead, on GitHub Pages.

## Publishing

Settings → Pages → Source: **Deploy from a branch**, branch `main`, folder `/` (root).

The URLs are then:

```
https://<username>.github.io/soccer-tactical-coach/support/
https://<username>.github.io/soccer-tactical-coach/privacy/
```

Paste those two into App Store Connect. **Open both in a private window first** — a support URL
that 404s is a rejection, and it is a slow one, because it comes back as a metadata note rather
than a build failure.

### Using the real domain instead

To serve these from `sportstablesoccercoach.com` — or a subdomain of it — add a file named
`CNAME` at the root of this repo containing the hostname, and point a DNS record at GitHub. The
DNS for that domain is at GoDaddy and records come with the domain registration rather than the
website plan, so the free site does not block it. Nothing in the pages needs changing: their
cross-links are relative, so they work at a domain root, on a subdomain, or in this project
subdirectory without edits.

## Editing

Each page is a **single self-contained file**. No stylesheet, font, script, image or analytics is
fetched from anywhere — deliberately, so a page cannot break because something else moved, and
because a privacy policy that phones out to a font CDN in order to say nothing is tracked is not
telling the truth. Keep it that way.

The privacy wording is mirrored in `PRIVACY.md` in the app repository. **Change both together**, and
update the "Last updated" date in the page when the policy itself changes rather than when the
markup does.

`.nojekyll` stops GitHub Pages running these through Jekyll. It is empty and should stay.

## What these pages claim

That the app collects nothing, has no accounts, no analytics and **no network use at all**. That is
true of the app as it stands, and it is the strongest thing the policy says. Anything added later
that reaches the internet — even a link out to a shop — means this wording has to be qualified
first. Do not add the feature and fix the page afterwards.
