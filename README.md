# auggie.dev

[![Netlify Status](https://api.netlify.com/api/v1/badges/89ca0414-26fa-420d-a9d3-fb7514b3a562/deploy-status)](https://app.netlify.com/sites/auggie/deploys)

The source for [auggie.dev](https://auggie.dev), Stephen Augustus's site and
blog. It's built with [Astro](https://astro.build), edited with
[TinaCMS](https://tina.io), and deployed on Netlify.

## Writing

- Posts live in `posts/` as Markdown, or can be edited in TinaCMS at
  `/admin`.
- The about page is `src/pages/about.md`.
- The site title and subtitle are in `src/settings/settings.json`.

### Bluesky comments

To show Bluesky replies as comments on a post:

1. Publish the post and share it on Bluesky.
1. Open the Bluesky post's single-post view by clicking its timestamp.
1. Build the URI as `at://<your-DID>/app.bsky.feed.post/<post-id>`.
1. Set it as the post's "Bluesky Post URI" in TinaCMS (`blueskyUri` in
   the front matter), then publish.

## Running locally

Use Node 22 (see `.nvmrc`).

| Command           | Action                                             |
| :---------------- | :------------------------------------------------- |
| `npm install`     | Install dependencies                               |
| `npm run dev`     | Start Astro and TinaCMS at `localhost:4321`        |
| `npm run build`   | Build TinaCMS and the production site to `./dist/` |
| `npm run preview` | Preview the build locally                          |

The CMS is at `localhost:4321/admin/index.html`. Building against Tina
Cloud needs a `.env.development` file with:

```sh
TINACLIENTID=<from tina.io>
TINATOKEN=<from tina.io>
TINASEARCH=<from tina.io>
```

## Credits

This site is built on [`blahg`](https://github.com/cassidoo/blahg), a blog
template by [Cassidy Williams](https://cassidoo.co/), with Bluesky comments
from [`uwu-tools/blahg-bsky`](https://github.com/uwu-tools/blahg-bsky). The
template's license is in [`LICENSE`](LICENSE).

To pull in later template changes, see
[`docs/upstream-sync.md`](docs/upstream-sync.md).
