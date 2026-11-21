# r10-cdn

Static assets served from Cloudflare Pages. Everything in `src/` is published as-is.

## Deployment

Cloudflare Pages is connected to this GitHub repository and deploys on push:

- push to `master` → production
- other branches / pull requests → preview deployment

### One-time setup

In **Workers & Pages → Create → Pages → Connect to Git**, pick this repository and set:

| Setting | Value |
| --- | --- |
| Production branch | `master` |
| Framework preset | None |
| Build command | *(empty)* |
| Build output directory | `src` |

The output directory is also set in [wrangler.toml](wrangler.toml). Then attach the custom domain under **Custom domains**.

## Local preview

```sh
npx wrangler pages dev
```

## Notes

- Pretty URLs (`/foo` → `foo.html`) are built into Pages.
- `src/404.html` is required: without it Pages falls back to SPA mode and serves `index.html` for every unknown path.
- Response headers live in `src/_headers`.
