# Invictus Supply Solutions LLC

The company's public, single-page website: **https://invictussupplysolutions.com/**.

Semantic HTML and CSS with original local SVG/PNG assets. No build system, runtime JavaScript, external fonts, analytics, or form service.

## Preview and edit

Run `python3 -m http.server 4173 --bind 127.0.0.1` in this directory, then open `http://127.0.0.1:4173/`.

- `index.html`: company copy, links, page metadata, and workflow illustration.
- `styles.css`: colors, typography, spacing, and responsive layouts.
- `assets/favicon.svg`: browser icon.
- `assets/social-card.svg`: editable source for the 1200 × 630 social-sharing PNG. Export to `assets/social-card.png` after visual changes.
- `CNAME`: intended custom domain for branch-based GitHub Pages publishing.

Keep factual claims aligned with the business's actual development stage. The DIBBS data-collection prototype is existing groundwork. Claude integration is planned. Do not add a formation year or certification claim without verification. Update the footer copyright year when appropriate.

## Publish

Repository: `Invictus-Supply-Solutions/Invictus-Supply-Solutions.github.io`.

GitHub Pages is configured to **Deploy from a branch**, branch **main**, folder **/ (root)**. `.nojekyll` keeps the site static. Publish an approved change by committing and pushing to `main`, subject to current repository protections. GitHub runs its managed **pages build and deployment** workflow; no custom workflow file is needed.

In **Settings → Pages**, the custom domain must be `invictussupplysolutions.com` and **Enforce HTTPS** must be enabled. `CNAME` supports this publishing method but is not proof that the live setting is configured.

The apex already uses GitHub's four A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, and `185.199.111.153`. At restoration, `www` uses Squarespace forwarding to the canonical HTTPS apex. This forwarding can remain while it works. To route `www` directly to Pages, change only its CNAME to `invictus-supply-solutions.github.io`, then verify the redirect and certificate. Preserve MX, SPF, DKIM, DMARC, domain verification records, and nameservers.

After publishing, confirm the Pages deployment succeeds for the intended commit, then check the actual public page, HTTPS, asset responses, HTTP redirect, and `www` forwarding. Do not infer public availability from a local preview alone.

## Verify changes

Before publishing, inspect desktop and mobile layouts, including narrow 320px screens. Check keyboard navigation and visible focus, all section anchors, both email links, reduced-motion behavior, and the absence of horizontal overflow. Ensure the social image and favicon load and the content distinguishes existing groundwork from planned capabilities.

Official GitHub guidance: [publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), [custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site), and [HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https).
