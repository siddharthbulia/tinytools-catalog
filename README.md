# tinytools-catalog

The public catalog of macOS apps shipped by [Sid Bulia](https://github.com/siddharthbulia).

Backing store for [tinytools.vercel.app](https://tinytools.vercel.app) — the cross-discovery site
for everything I've shipped via my [app-factory](https://github.com/siddharthbulia) workflow.

## What's here

Just one file: [`apps.json`](./apps.json).

It lists every app I've shipped, with: name, tagline, description, current version, download URLs
(arm64 + x64), website, price tier (free or free + pro), Stripe Buy URL where applicable, icon gradient, etc.

Schema is versioned (`"version": 1`). I'll bump the version when the shape changes in a
backwards-incompatible way; consumers should pin themselves to a known version.

## Consuming the catalog

```bash
curl https://raw.githubusercontent.com/siddharthbulia/tinytools-catalog/main/apps.json
```

For lower latency, mirror via a Cloudflare Worker or proxy your own.

## How it's generated

This repo is updated by `scripts/update-catalog.js` in my [app-factory](https://github.com/siddharthbulia)
workflow. After every app release, I run:

```bash
node scripts/update-catalog.js --push
```

That reads each app's `app.config.json` + `package.json`, HEAD-fetches the DMG to record sizes,
and rewrites `apps.json` here. No CI yet — that's a v1.1 candidate.

## License

The catalog itself (the JSON) is CC0 — public domain. The apps it points to have their own licenses.

## Why a catalog repo, not an app store?

Because every Mac app's wedge feature for "cross-discovery" turns out to be undercut by Sparkle
(per-app auto-update). A flat catalog JSON + a small landing page that renders it is the right
floor for the problem. If the data later justifies it, a real Mac app store can read from this
same JSON.

See [tinytools.vercel.app](https://tinytools.vercel.app) for the rendered version.
