# Invictus Supply Solutions LLC websites

Maintain both static sites in this project. The company root page and the innovation consultancy page have separate public addresses and GitHub Pages deployments.

| Website | Source here | Publishing repository |
| --- | --- | --- |
| https://invictussupplysolutions.com/ | Root `index.html`, `styles.css`, `assets/` | `Invictus-Supply-Solutions/Invictus-Supply-Solutions.github.io` |
| https://innovation.invictussupplysolutions.com/ | `innovation/` | `Invictus-Supply-Solutions/invictus-innovation` |

The root page and its procurement social-card assets are retained. The innovation page describes an exploratory consultancy; examples are proposed workflows, not customer results or launched products.

## Preview and edit

From this directory run:

```sh
python3 -m http.server 4177 --bind 127.0.0.1
```

Open `http://127.0.0.1:4177/` for the root site and `http://127.0.0.1:4177/innovation/` for the consultancy. Stop the server with Ctrl-C when finished.

Edit the appropriate `index.html` for copy and `styles.css` for appearance. Both sites work without a package installation or build step. Keep private records and credentials out of these public files. Screenshots and verification records belong in the ignored `artifacts/` folder.

## Publish approved changes

Review the diff and check phone and desktop layouts before committing. Work on a change branch; after approval, bring the reviewed change into canonical `main` using the repository's current rules.

Publishing the root project:

```sh
git push origin main
```

Publishing the innovation folder, from a clean, reviewed `main` checkout:

```sh
git subtree push --prefix=innovation https://github.com/Invictus-Supply-Solutions/invictus-innovation.git main
```

The second command publishes only committed files under `innovation/`. A root push alone does not update the separate innovation hostname. The innovation repository is a publication copy; make edits in this canonical project, not directly in that copy. If the mirror has independent changes, reconcile them here before publishing; do not force-push to bypass a divergence.

Both repositories use Pages **Deploy from a branch**, `main`, `/ (root)`. Retain `.nojekyll` and the correct `CNAME` in each source root. Verify both Pages runs and public URLs after deployment. Pages custom-domain settings must also match; a local file alone is not proof of live configuration.

## Domains and email

The root stays at `invictussupplysolutions.com`. The innovation site uses `innovation.invictussupplysolutions.com`, with a DNS CNAME for host `innovation` pointing to `invictus-supply-solutions.github.io`. Keep HTTPS enforced for both.

Retain the root site's apex records and existing `www` forwarding. Preserve domain registration, nameservers, MX, SPF, DKIM, DMARC and verification records. The email contact remains `philip@invictussupplysolutions.com` on both pages.

`innovation/` is also accessible as a path on the root site; its canonical metadata identifies the subdomain as the preferred address. See [publication configuration](docs/publication-options.md).

## Verification

Check the two distinct page headings, local CSS/favicon assets, navigation anchors, keyboard focus, email links, narrow-screen wrapping, and HTTPS. Keep the original root social-card assets: the original page references them. The innovation site uses text-only social metadata.

Official guidance: [publishing sources](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), [custom domains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).
