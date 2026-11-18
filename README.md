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

Review the diff and check phone and desktop layouts on a change branch. Open a pull request against canonical `main`. After review and any configured checks pass, merge it in GitHub. GitHub Pages publishes the company root from that branch.

### Update the separate innovation site

When an approved change touches `innovation/`, run the following from a clean checkout of this canonical repository. Its `origin` should point to the company repository. The commands use the merged source on canonical `main` and start a review branch from the mirror's current `main`.

```sh
mirror_url=https://github.com/Invictus-Supply-Solutions/invictus-innovation.git
review_ready=false
git fetch origin refs/heads/main &&
source_commit=$(git rev-parse FETCH_HEAD) &&
source_short=$(git rev-parse --short=12 "$source_commit") &&
split_commit=$(git subtree split --prefix=innovation "$source_commit") &&
split_tree=$(git rev-parse "$split_commit^{tree}") &&
git fetch "$mirror_url" refs/heads/main &&
mirror_base=$(git rev-parse FETCH_HEAD) &&
mirror_tree=$(git rev-parse "$mirror_base^{tree}") &&
if [ "$split_tree" = "$mirror_tree" ]; then
  printf '%s\n' 'The innovation mirror is already current.'
else
  review_dir=$(mktemp -d "${TMPDIR:-/tmp}/invictus-publish.XXXXXX") &&
  review_branch="publish/innovation-$source_short-${review_dir##*.}" &&
  git worktree add -b "$review_branch" "$review_dir" "$mirror_base" &&
  git -C "$review_dir" merge --no-ff --no-edit "$split_commit" &&
  test "$(git -C "$review_dir" rev-parse 'HEAD^{tree}')" = "$split_tree" &&
  git -C "$review_dir" diff "$mirror_base" HEAD -- &&
  review_ready=true
fi
```

If the first block reports that the mirror is current, stop there. If the merge conflicts, run `git -C "$review_dir" merge --abort`. Remove the worktree once it is clean with `git worktree remove "$review_dir"`. A tree mismatch means the resulting snapshot contains a difference from the canonical subtree. Reconcile that difference in the canonical repository before retrying. Each retry creates a fresh review branch and worktree.

After reviewing the diff, push the prepared branch from the same shell.

```sh
test "$review_ready" = true &&
test "$(git -C "$review_dir" rev-parse 'HEAD^{tree}')" = "$split_tree" &&
git -C "$review_dir" push "$mirror_url" "HEAD:refs/heads/$review_branch"
```

Open a pull request from that branch into `main` in [the innovation repository](https://github.com/Invictus-Supply-Solutions/invictus-innovation). Note the canonical source commit in the PR. If the mirror base advances during review, prepare a fresh branch from the updated base and verify the diff again. Once approved, use **Create a merge commit** so the next subtree split retains its ancestry. You can remove the clean local worktree with `git worktree remove "$review_dir"`.

Both repositories use Pages **Deploy from a branch**, `main`, `/ (root)`. Retain `.nojekyll` and the correct `CNAME` in each source root. Verify the relevant Pages run and public URL after publishing. Pages custom-domain settings must also match the expected domain.

## Domains and email

The root stays at `invictussupplysolutions.com`. The innovation site uses `innovation.invictussupplysolutions.com`, with a DNS CNAME for host `innovation` pointing to `invictus-supply-solutions.github.io`. Keep HTTPS enforced for both.

Retain the root site's apex records and existing `www` forwarding. Preserve domain registration, nameservers, MX, SPF, DKIM, DMARC and verification records. The email contact remains `philip@invictussupplysolutions.com` on both pages.

`innovation/` is also accessible as a path on the root site; its canonical metadata identifies the subdomain as the preferred address. See [publication configuration](docs/publication-options.md).

## Verification

Check the two distinct page headings, local CSS/favicon assets, navigation anchors, keyboard focus, email links, narrow-screen wrapping, and HTTPS. Keep the original root social-card assets: the original page references them. The innovation site uses text-only social metadata.

Official guidance: [publishing sources](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site), [custom domains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).
