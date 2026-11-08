# Pulling in upstream template changes

This site is built on [`cassidoo/blahg`](https://github.com/cassidoo/blahg).
Since 2026-11, `main` shares history with it, so taking upstream changes
is an ordinary merge.

## 1. Merge upstream

```sh
git remote add upstream https://github.com/cassidoo/blahg.git  # once per clone
git fetch upstream
git switch -c upstream-sync-$(date +%Y%m%d) origin/main
git merge upstream/main
```

## 2. Resolve conflicts

- **This site's own files:** keep this site's version of `README.md`,
  `src/pages/about.md`, `src/settings/settings.json`,
  `src/components/Header.astro`, `astro.config.mjs`, and
  `public/robots.txt`. Carry over any new setup steps that apply.
- **`posts/`:** delete any example posts upstream adds (`git rm`). Only
  this site's posts belong here.
- **Bluesky comments:** upstream doesn't have this feature. In
  `src/layouts/BlogPost.astro`, `src/components/CommentSection.astro`,
  `tina/config.js`, and `src/content.config.js`, keep
  `CommentSection`, the `blueskyUri` Tina field, and
  `blueskyUri: z.string().optional()` in the content schema. Without
  the schema line, comments silently stop rendering.
- **`package.json`:** take upstream's new dependencies, keep the newer
  version of each package, and keep the `overrides` block.
- **`package-lock.json` and `tina/tina-lock.json`:** take either side,
  then regenerate them with `npm install`.
- **`LICENSE`:** take upstream's.

## 3. Check it

Use the Node version in `.nvmrc`, and confirm it still meets the
`engines.node` range of the new Astro version.

```sh
npm install
npm audit
npx tinacms build --local --skip-cloud-checks
npx astro build
```

- Both builds exit 0.
- `dist/post/bsky-comments/` exists and the post page loads its
  Bluesky comments.
- No upstream example posts appear under `dist/post/`.
- Note any remaining `npm audit` findings, and why they remain, in the
  PR description.

## 4. Open the PR

Push the branch and open a PR. Netlify's deploy preview runs the
production `tinacms build` against Tina Cloud. Read its deploy log
before merging, since Tina Cloud credential and schema problems show up
only there. Merging to `main` deploys the site.
