# Publication configuration — October 7, 2026

Decision: deploy both pages. The existing company root page remains at `invictussupplysolutions.com`; the consultancy page is published separately at `innovation.invictussupplysolutions.com`. The earlier either/or proposal is superseded.

## Source and deployments

The canonical project is the existing Invictus checkout and `Invictus-Supply-Solutions/Invictus-Supply-Solutions.github.io` repository. Root HTML, CSS, domain files and assets retain the original company site. The `innovation/` folder contains the reviewed consultancy site with its own metadata, favicon, domain file, robots file and sitemap.

A separate public Pages repository, `Invictus-Supply-Solutions/invictus-innovation`, receives the Git subtree split of `innovation/`. This gives each hostname its own Pages configuration without a second editable source tree, paid service, framework, build dependency, cross-repository workflow token or scheduled automation. The README contains the two publication commands.

| Setting | Company root | Innovation |
| --- | --- | --- |
| Source repository | `Invictus-Supply-Solutions.github.io` | `invictus-innovation` |
| Pages branch / folder | `main` / `/` | `main` / `/` |
| Custom domain | `invictussupplysolutions.com` | `innovation.invictussupplysolutions.com` |
| DNS | Existing apex records retained | CNAME `innovation` to `invictus-supply-solutions.github.io` |
| HTTPS | Enforced | Enforce once certificate is ready |

Set the innovation Pages custom domain before adding its DNS record. A specific CNAME is used; no wildcard is needed. GitHub's documented automatic redirects for a hostname and its `www` variant do not make arbitrary subdomains aliases of the company root site. [GitHub domain setup](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

GitHub supports a project site's own custom domain alongside its organization's site. [Custom domains across repositories](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)

Preserve root `www` forwarding, domain registration and all email records. No legal-name, account, insurance, card, procurement-system or Workspace change is part of this deployment.

## Validation and ongoing changes

Check both page contents and deployment revisions independently. Record successful public HTTP responses, certificate validity, enforced HTTPS and working local assets. DNS/certificate propagation may delay the new hostname after a successful Pages build; report those states separately.

Make future edits in this canonical project. Publish only committed, reviewed innovation source through the subtree command. GitHub settings may write a CNAME commit in the publication repository; reconcile any independent mirror commit before later pushes rather than overwriting it. Keep the original root social-card assets because the root HTML references them.
