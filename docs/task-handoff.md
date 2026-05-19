# Task Handoff — FeedBack-site

## Current Deployment Status

Live at: `https://feedbex.ai`

Deployed via GitHub Pages. No build step — a git push to this repo is all it takes to go live.

## What's Live

- Landing page (`index.html`) — includes the "Connect Instagram" button that initiates the OAuth flow for client onboarding
- Privacy policy (`privacy.html`) — required by Meta for App Review
- Terms of service (`terms.html`) — required by Meta for App Review
- CSS token system (`css/tokens.css`) — all design tokens (colors, spacing, typography)

## What's Pending

No active work needed. This site only needs updates when:
- A product requires a new page (e.g. a new OAuth flow for Google Reviews onboarding)
- The Instagram OAuth flow changes (e.g. redirect URI, state param, scopes)
- Meta requires additional pages for App Review

## Future Migration Note

When this site moves to a new repo (e.g. `FeedBex/FeedBex_site`), make sure the website moves with it:
1. Copy all site files to the new repo
2. Add the `CNAME` file (containing `feedbex.ai`) to the new repo root
3. In the new repo's GitHub Pages settings → set `feedbex.ai` as the custom domain
4. In the old repo's GitHub Pages settings → remove the custom domain
5. Enable Enforce HTTPS on the new repo

GoDaddy DNS does not need to change — it always points to GitHub regardless of which repo is active.
