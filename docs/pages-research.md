# Invictus GitHub Pages restoration research

Observed 2026-10-07 using public DNS via Cloudflare `1.1.1.1` and unauthenticated HTTP requests. No DNS or repository settings were changed. Parent orientation consumed Harness `main` revision `bcfb9b382816c5a0deb06e99f67bb3ea805a288e`.

## Current public state

| Name / record | Observed value |
| --- | --- |
| Apex A | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` (TTL 1800) |
| Apex AAAA / CNAME / CAA | No answers; DNS status `NOERROR` |
| Apex NS | `ns-cloud-a1.googledomains.com`, `ns-cloud-a2.googledomains.com`, `ns-cloud-a3.googledomains.com`, `ns-cloud-a4.googledomains.com` |
| www CNAME | `ext-sq.squarespace.com` (TTL 14400) |
| www resolved A | `198.185.159.144`, `198.185.159.145`, `198.49.23.144`, `198.49.23.145` |
| www AAAA | CNAME returned, no IPv6 answer |

| URL | Status | Redirect |
| --- | --- | --- |
| `http://invictussupplysolutions.com/` | 404 | None |
| `https://invictussupplysolutions.com/` | 404 | None |
| `http://www.invictussupplysolutions.com/` | 301 | `https://invictussupplysolutions.com/` |
| `https://www.invictussupplysolutions.com/` | 301 | `https://invictussupplysolutions.com/` |

Both HTTPS requests passed curl's normal certificate verification. Apex already routes to the documented GitHub Pages IPv4 addresses. The failure therefore is not an apex address mismatch. Repository Pages settings, source content and deployment still require inspection. `www` currently routes through Squarespace, which forwards to the failing apex.

Initial sandboxed network probes were blocked by the local execution sandbox; the values above come from successful approved public network reads, not those failed probes.

## Current GitHub procedure

For a plain static site, choose repository **Settings → Pages → Build and deployment → Deploy from a branch**, then the existing branch and `/` or `/docs`. Use GitHub Actions when a custom build is needed. Check the resulting Pages workflow run. A workflow-based site still needs its custom domain set through Pages settings/API; a `CNAME` file alone does not configure it. [Publishing source documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

Configure `invictussupplysolutions.com` in Pages before pointing new DNS records there. Branch publishing writes a `CNAME` file at the publishing root; custom Actions publishing ignores that file. Keep apex A records above. Optional IPv6 records are `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, and `2606:50c0:8003::153`; retain IPv4 when adding IPv6. `ALIAS`/`ANAME` to the Pages default hostname is an alternative.

For `www`, replace the Squarespace CNAME with the verified repository owner's `<owner>.github.io` hostname, excluding the repository name. Do not infer that owner until the repository is identified. Correct apex and `www` records let Pages handle canonical redirects. GitHub recommends domain verification and avoiding wildcard records. DNS changes can take 24 hours. [Custom domain documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

Saving a custom domain starts a DNS check and, if successful, automatic Let's Encrypt certificate issuance. Select **Enforce HTTPS** in Pages when available, then verify the HTTP redirect, valid TLS, public content, and HTTPS assets. Extra conflicting apex or `www` records can prevent certificate issuance. If issuance stalls after several minutes, GitHub documents removing/re-adding the custom domain to restart provisioning; do this only when necessary and authorized. [HTTPS documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)

## Restoration decision

Authenticated GitHub reads confirmed the account `philiprabe` is an active administrator of `Invictus-Supply-Solutions`. The organization reported zero public and zero private repositories. Searches through the CLI and GitHub connector found no recoverable current website repository. The local workspace was empty, with no repository history or brand assets. These observations establish the missing current publishing repository, but do not establish when or why an earlier repository disappeared.

The owner's 2026-10-07 request explicitly authorized creating a dedicated website repository if recovery was unavailable and publishing to GitHub Pages. The new public repository is `Invictus-Supply-Solutions/Invictus-Supply-Solutions.github.io`. Its repository ruleset response was empty. No existing repository visibility, application code, DNS record, or email configuration was changed.

The selected implementation is static HTML/CSS with branch-based Pages publishing from `main` at `/`. Apex A records are retained. `www` forwarding remains in place. A future direct Pages route would change only `www` CNAME from `ext-sq.squarespace.com` to `invictus-supply-solutions.github.io`; that change is optional while the existing redirect works. See repository deployment history for the published revision and README for maintenance and verification steps.
