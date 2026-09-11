# HTTP2XX Test App (Pure Native OIDC)

A vendor-agnostic, zero-dependency Single-Page Application demonstrating authentication using standard **OpenID Connect Core 1.0** and **OAuth 2.0 Authorization Code Flow with PKCE (RFC 7636)**.

Designed to run statically on **GitHub Pages** with custom domain support (`logto-test.http2xx.io`).

---

## ⚡ Zero Vendor Lock-in

This application uses **zero proprietary vendor SDKs**. It interacts with the identity provider using pure standard protocols and standard browser Web APIs:

* **PKCE (Proof Key for Code Exchange)** via standard `window.crypto.subtle` (SHA-256)
* **OIDC Discovery** via standard `/.well-known/openid-configuration`
* **Authorization & Token Exchange** via standard OIDC `/oidc/auth` and `/oidc/token`
* **UserInfo Endpoint** via standard Bearer token `GET /oidc/me`
* **RP-Initiated Logout** via standard `end_session_endpoint`

You can point this app to **Logto**, **Keycloak**, **Auth0**, **Okta**, **Zitadel**, or any compliant OIDC provider without changing a single line of code.

---

## 🌐 Endpoints & Configuration

### Logto Console Setup
1. In Logto Console, navigate to **Applications** > **Create application**.
2. Select **Single Page App (SPA)**.
3. Configure the endpoints:
   - **Redirect URIs**: `https://logto-test.http2xx.io/callback` (and `http://localhost:3000/callback` for local testing)
   - **Post sign-out redirect URIs**: `https://logto-test.http2xx.io/`
   - **CORS / Allowed Origins**: `https://logto-test.http2xx.io` (and `http://localhost:3000`)
4. Copy your **App ID** (Client ID).

### App In-Browser Configuration
Click the **⚙ Config** button in the header of the app to set or adjust:
* **Client ID / App ID**: Your Logto App ID.
* **OIDC Issuer**: Default is `https://auth.allsrc.dev/oidc`.
* **Scopes**: Default is `openid profile email`.

---

## 🚀 GitHub Pages Deployment

The repository is structured for direct static hosting on GitHub Pages:

| File | Purpose |
| :--- | :--- |
| `index.html` | The primary SPA application (Single-file HTML + JS + CSS). |
| `404.html` | Direct duplicate of `index.html` enabling GitHub Pages to route `/callback` directly into the SPA without 404 errors. |
| `CNAME` | Binds GitHub Pages to your custom domain `logto-test.http2xx.io`. |
| `.nojekyll` | Prevents GitHub Pages from running Jekyll transformations. |
| `_redirects` | Fallback SPA rewrite rule (`/* /index.html 200`) for Cloudflare Pages / Netlify / Vercel. |

### Enabling GitHub Pages in GitHub:
1. Push this repository to GitHub (`main` branch).
2. Go to repository **Settings** > **Pages**.
3. Under **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: `main` / `/(root)`
4. Under **Custom domain**:
   - Enter: `logto-test.http2xx.io`
   - Ensure DNS CNAME points `logto-test.http2xx.io` to `<your-username>.github.io`.
   - Enforce HTTPS.
