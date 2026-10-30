# living.codes

Front page of the **Living Codes Lab** — the research group of Erik Garrison
(University of Tennessee Health Science Center, Memphis, TN, and the network).

A single static `index.html`. No framework, no build step, no dependencies beyond
two Google Fonts. Dark by default, follows the system theme, with a manual
auto → dark → light toggle in the header.

## Deploy (GitHub Pages)

Exactly the `poietic.life` pattern:

1. Push this directory as the repo root (branch `main`).
   The `CNAME` file must stay — it pins the custom domain.
2. Repo → Settings → Pages → Custom domain: `living.codes`, enforce HTTPS.
3. Cloudflare DNS (the domain lives there), **DNS only / grey cloud**:

   | Type | Name | Content |
   |------|------|---------|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | AAAA | `@` | `2606:50c0:8000::153` |
   | AAAA | `@` | `2606:50c0:8001::153` |
   | AAAA | `@` | `2606:50c0:8002::153` |
   | AAAA | `@` | `2606:50c0:8003::153` |
   | CNAME | `www` | `<account>.github.io` (optional) |

   GitHub serves the TLS certificate; don't proxy through Cloudflare (orange
   cloud) unless you also want to manage SSL termination there. DNS-only is the
   simple, working setup — it's what `poietic.life` uses.

## Subdomains on the lab server (ulivo)

For heavier things that shouldn't live on GitHub Pages — apps, API endpoints,
large artifacts — point a subdomain at the lab server, the same way
`ulivo.poietic.life` works:

1. Cloudflare: **A** record `<name>.living.codes` → `136.243.177.252`, DNS only.
2. On ulivo, add `/etc/nginx/sites-available/<name>.living.codes` mirroring the
   `ulivo.poietic.life` vhost (root under `/var/www/<name>.living.codes`),
   symlink into `sites-enabled`.
3. `sudo certbot --nginx -d <name>.living.codes` for TLS.

## Editing

- All content is in `index.html` — text is in plain HTML, styles inline in
  `<head>`. The hero graph and the favicon are hand-drawn inline SVG.
- Publications list: keep the role annotations honest (who corresponding,
  co-conceived, etc.) — that discipline is part of the site's voice.
- `assets/ekg.jpg` is the GitHub avatar, self-hosted for reliability.
