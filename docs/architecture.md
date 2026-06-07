# Architecture — FeedBack-site

## Deployment

Static site hosted on GitHub Pages (`FeedBackv1/FeedBack-site` repo). No framework, no build step, no server.

- **URL:** `https://feedbex.ai`
- **Custom domain:** `feedbex.ai` (registered on GoDaddy). CNAME file in repo root points GitHub Pages to this domain. GoDaddy DNS has 4 A records pointing to GitHub's servers and a `www` CNAME pointing to `feedbackv1.github.io`.

### How to deploy (do NOT push to FeedBack-site directly)

All edits happen in the **FeedBex repo** (`FeedBackv1/FeedBex`), inside the `FeedBack-site/` folder.
When you push to FeedBex master, a GitHub Actions workflow (`.github/workflows/deploy-site.yml`) automatically copies this folder to the `FeedBack-site` repo → GitHub Pages deploys it live within seconds.

**Deploy token:** A GitHub PAT named `DEPLOY_TOKEN` is stored in FeedBex repo → Settings → Secrets → Actions.
- **Expires:** 2026-10-31
- **Scope:** `repo`
- **When it expires:** Generate a new token at GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic). Replace the secret value in FeedBex → Settings → Secrets → DEPLOY_TOKEN. Next time create with no expiration.

---

## Page Inventory

| File | Purpose |
|------|---------|
| `index.html` | Landing page. Contains the "Connect Instagram" button that initiates the OAuth onboarding flow for new clients. |
| `privacy.html` | Privacy policy. Required by Meta for App Review. |
| `terms.html` | Terms of service. Required by Meta for App Review. |
| `css/tokens.css` | All design tokens — colors, spacing, typography. Edit here, never inline. |

---

## OAuth Flow (Instagram Onboarding)

The "Connect Instagram" button on `index.html` initiates the Instagram OAuth flow for the DM Auto-Reply module.

**Critical:** The `state` parameter in the OAuth URL must be set to the client's `internalBusinessKey`. This is how the OAuth callback workflow (`Instagram OAuth Redirect`, ID: `XFldtbNYlKJLwrms`) knows which row in Google Sheets to write the token to. If the `state` param is missing or wrong, the onboarding fails silently.

The OAuth callback is handled entirely in n8n — the site only generates the authorization URL. Full OAuth flow details are in `DM_IG_Auto-Responder/docs/oauth-strategy.md`.

---

## CSS Token System

All visual design is controlled through `css/tokens.css`. Do not add inline styles or hardcode colors, spacing, or typography anywhere in the HTML. Edit the token file and let the cascade handle the rest.
