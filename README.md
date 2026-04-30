# ghost

A private iOS journal for the messages you write but never send.
Local-only, no servers, no analytics. iPhone, iOS 17+.

## What's in this repo

| Path | Purpose |
|---|---|
| [`pages.html`](pages.html) | Marketing landing page. Deployed as `/index.html`. |
| [`legal/`](legal/) | Privacy policy, Terms, EULA, and the imagined-reply disclosure for App Review. Deployed as-is. |
| [`launch/`](launch/) | App Store Connect cheat sheet + launch kit. **Not** deployed. |
| [`GHOST/`](GHOST/) | iOS app source (SwiftUI, single target). |
| [`GHOST.xcodeproj/`](GHOST.xcodeproj/) | Xcode project. |
| [`.github/workflows/pages.yml`](.github/workflows/pages.yml) | Auto-deploys `pages.html` + `legal/` to GitHub Pages on push to `main`. |

## Deploying the site

1. Push the repo to GitHub.
2. Repo → **Settings** → **Pages** → Source: **GitHub Actions**.
3. Push to `main` (or run the workflow manually from the Actions tab). After ~90s the site is live at `https://<user>.github.io/<repo>/`.
4. **Custom domain (optional):** uncomment the `CNAME` line in `.github/workflows/pages.yml`, set it to your domain, configure DNS as GitHub instructs, re-deploy.

The workflow only publishes `pages.html` (renamed to `index.html`) and `legal/`. Swift sources, the Xcode project, and `launch/` stay private.

## Building the iOS app

```bash
xcodebuild -project GHOST.xcodeproj -scheme GHOST \
  -destination 'generic/platform=iOS Simulator' build
```

Or open `GHOST.xcodeproj` in Xcode and ⌘R.

### One-time Xcode setup before App Store submission

- **Edit Scheme → Run → Options → StoreKit Configuration:** select [`GHOST/Subscription/Products.storekit`](GHOST/Subscription/Products.storekit).
- **Signing & Capabilities → Team:** set to your Apple Developer team.
- **App Store Connect:** create the bundle ID `app.ghost.ios` and the non-consumable IAP `app.ghost.ios.unlock` ($9.99) before you upload a build.

## App Store submission checklist

See [`launch/app-store-listing.md`](launch/app-store-listing.md). Reviewer notes are in the same file under §8 — copy them verbatim into App Store Connect.

The imagined-reply feature is documented in detail at [`legal/imagined-reply-disclosure.html`](legal/imagined-reply-disclosure.html); App Reviewers will be pointed at this URL.

## License

App: © 2026, all rights reserved. See [`legal/eula.html`](legal/eula.html) and [`legal/terms.html`](legal/terms.html).
