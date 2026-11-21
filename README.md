# r10-cdn

Static assets served from Cloudflare Workers (static assets, no Worker script). Everything in `src/` is published as-is.

## Deployment

Cloudflare Workers Builds is connected to this GitHub repository and deploys on push:

- push to `master` → production
- other branches → preview version

### One-time setup

In **Workers & Pages → Create → Import a repository**, pick this repository and set:

| Setting | Value |
| --- | --- |
| Production branch | `master` |
| Build command | *(empty)* |
| Deploy command | `npx wrangler deploy` |
| Non-production branch deploy command | `npx wrangler versions upload` |

Configuration lives in [wrangler.toml](wrangler.toml). Then attach the custom domain under **Settings → Domains & Routes**.

## Local preview

```sh
npx wrangler dev
```

## Notes

- Pretty URLs (`/foo` → `foo.html`) are handled by the default `html_handling` mode.
- Unknown paths are served `src/404.html` with a 404 status (`not_found_handling = "404-page"`).
- Response headers live in `src/_headers`.
