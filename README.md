# IE Aware

A minimal, responsive links-only homepage for the Inland Empire. Plain HTML and CSS served by Cloudflare Workers Static Assets. No application build step, browser JavaScript, or Worker script is required. Visual theming is intentionally deferred.

## Local development

Install Node.js 22 or newer, then run from this repository:

```sh
npm ci
npm run dev
```

Open the local URL printed by Wrangler (normally http://localhost:8787).

## Validate and deploy

```sh
npm run check
npx wrangler login
npm run deploy
```

`check` validates the deployment configuration with a dry run; it does not publish the site. Deployment requires your Cloudflare account and prints the deployed URL. The Worker name is `ieaware-home`; change it in `wrangler.jsonc` if needed before deployment.

For Cloudflare Workers Git builds, leave the build command empty and use `npm run deploy` as the deploy command, with this repository as the root directory. There is no generated output directory: Wrangler uploads `public/` directly.

To connect a domain you own, open the Worker in Cloudflare and use **Settings > Domains & Routes > Add > Custom Domain**. No custom domain is assumed in this repository.

## Update links

Edit the list in `public/index.html`. Duplicate an existing `<li>` for each verified city website, updating its HTTPS URL, name, and city. FontanaAware at https://fontanaware.org is the user-supplied destination. No other city sites are assumed or advertised. Edit `public/styles.css` when ready to develop the visual theme.

Only files in `public/` are published. Keep private files and credentials outside it. Unknown paths return 404 rather than the homepage.

## Files

- `public/index.html` — page content and city links
- `public/styles.css` — neutral responsive layout and keyboard focus styling
- `wrangler.jsonc` — Cloudflare Static Assets configuration
- `package.json` / `package-lock.json` — local and deployment commands, pinned tooling

Reference: [Cloudflare Workers Static Assets](https://developers.cloudflare.com/workers/static-assets/get-started/).
