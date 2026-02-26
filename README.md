# RGL Client Intake

**Rebel Growth Labs** — Client Integration Onboarding Portal

This project powers the secure client credential intake and OAuth authorization flow for the Rebel Growth Labs BLAST Framework integration stack.

---

## What This Does

Guides clients through authorizing third-party platform access (Square, Meta) so Rebel Growth Labs can build and manage their revenue attribution infrastructure — without clients needing to manually copy or paste API credentials.

---

## Stack

- Vanilla HTML / CSS / JS — zero framework dependencies
- Vercel — hosting and serverless functions
- Square OAuth 2.0 — secure seller account authorization
- Meta OAuth — Facebook Business / Ad Account authorization
- Formspree — credential delivery to RGL team

---

## Project Structure

```
rgl-client-intake/
├── index.html          # Main client-facing OAuth authorization page
├── callback.html       # OAuth callback handler (Square + Meta)
├── success.html        # Post-authorization confirmation screen
└── README.md
```

---

## Deployment

This project is deployed via Vercel. Every push to `main` triggers an automatic deployment.

```bash
git add .
git commit -m "update"
git push origin main
```

---

## Environment Variables

Set these in Vercel project settings before deploying:

| Variable | Description |
|---|---|
| `SQUARE_APP_ID` | Square Production Application ID |
| `SQUARE_APP_SECRET` | Square OAuth Application Secret |
| `META_APP_ID` | Meta / Facebook App ID |
| `META_APP_SECRET` | Meta App Secret |
| `FORMSPREE_ENDPOINT` | Formspree form endpoint URL |

---

## OAuth Flow

### Square
1. Client clicks **Connect Square**
2. Redirected to Square authorization page
3. Client logs in and clicks Allow
4. Square redirects back to `/callback` with authorization code
5. Server exchanges code for access token
6. Token delivered to RGL team via Formspree

### Meta
1. Client clicks **Connect Facebook**
2. Redirected to Facebook OAuth dialog
3. Client approves requested permissions
4. Facebook redirects back to `/callback` with authorization code
5. Server exchanges code for access token
6. Token delivered to RGL team via Formspree

---

## Permissions Requested

### Square
- `CUSTOMERS_READ`
- `PAYMENTS_READ`
- `ORDERS_READ`
- `MERCHANT_PROFILE_READ`
- `INVOICES_READ`
- `SUBSCRIPTIONS_READ`
- `CATALOG_READ`

### Meta
- `ads_read`
- `business_management`
- `ads_management`

---

## Security

- All tokens transmitted via HTTPS only
- No credentials stored client-side
- OAuth state parameter used to prevent CSRF attacks
- Tokens delivered directly to RGL team — never logged or stored on server

---

*Rebel Growth Labs · rebelgrowthlabs.com · Confidential*
