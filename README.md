# corp-web-maintenance-vzs

Static "under maintenance" page for **VerzuimSignaal**.

## Purpose

This is a single, self-contained HTML file that is deployed in place of the
regular VerzuimSignaal website when the application needs to go **fully
offline** for major maintenance (e.g. infrastructure migrations, database
upgrades).

During such a window, the site's DNS record is pointed at wherever this page
is hosted so visitors see a clear "we'll be back" message instead of a
broken site or a generic error page.

## How it works

- `index.html` is fully self-contained: the heading font and logo are
  embedded as base64 data URIs, and all styling is inline `<style>` — there
  are no external requests, so the page works even if other infrastructure
  (CDN, DNS for subdomains, etc.) is degraded.
- `<meta name="robots" content="noindex">` keeps the page out of search
  results.
- The page can be hosted anywhere that can serve a static file (S3 + a
  static site endpoint, Netlify, Vercel, Cloudflare Pages, a plain nginx
  box, etc.).

## Usage

1. Update the maintenance window text and support email in `index.html` if
   the details differ from the current placeholders.
2. Deploy `index.html` to your static host of choice.
3. Point the relevant DNS record(s) at that host for the duration of the
   maintenance window.
4. Revert the DNS record(s) back to the regular application once
   maintenance is complete.

## Notes

- Layout, spacing, and structure are kept in sync with the sibling
  maintenance page for BlueVi (`corp-web-maintenance-bluevi`) — only
  branding (logo, colors) and copy differ.
