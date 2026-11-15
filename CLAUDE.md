# ShopDesk marketing site (shopdesk.site)

Static site hosted on Netlify (site `gentle-clafoutis-20123c`), behind Cloudflare DNS. The owner dashboard is `shopdesk-dashboard` (app.shopdesk.site); the booking backend is `shopdesk-booking`.

## Only `public/` is published

`netlify.toml` publishes `public/` and nothing else. Never put notes, sales material, plans, scripts, `package.json`, `node_modules` or config in `public/`. Until November 2026 the site was deployed by dragging a whole working folder into Netlify, which made the sales playbook, business plans and a script with an API key publicly readable. CI blocks non-web files and obvious secrets in `public/`.

Never deploy by drag-and-drop or `netlify deploy` from a local folder. Production deploys come only from `main`.

## How we work

1. Branch off an up-to-date `main`: `git switch main && git pull && git switch -c <type>/<short-name>`.
2. One logical change per branch. Commit with `git commit -F <file>`, conventional style (`fix: …`, `feat: …`), body explains why.
3. Push and open a PR with `gh pr create`. Netlify posts a deploy preview; check the change there.
4. Merge only after CI (`check`) is green: `gh pr merge --squash --delete-branch`.
5. After merge, confirm the change on https://shopdesk.site.

## Content rules

- Prices, call allowances and overage must match the dashboard's plan step (`shopdesk-dashboard/src/components/onboarding/PlanSelectionStep.tsx`): Starter $99 / 150 calls, Pro $229 / 400 calls, Growth $499 / 1,000 calls, $0.99 per additional call.
- Features that aren't built are labeled "(coming soon)".
- No fake phone numbers or results presented as real. Sample screens are labeled as examples.
- Security headers live in `public/_headers`. If you add an external resource (fonts, analytics, video), update the Content-Security-Policy there.
