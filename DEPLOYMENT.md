# Deploy the public homepage

## Current settings

| Setting | Value |
| --- | --- |
| GitHub organization | `review-audit` |
| Repository | `review-audit.github.io` (public) |
| Pages source | Deploy from a branch |
| Branch / directory | `main` / `/ (root)` |
| HTTPS | Enforced |
| Custom domain | None |
| Website | https://review-audit.github.io/ |
| Sign-in destination | https://review-audit-seven.vercel.app/ |
| Registration destination | https://review-audit-seven.vercel.app/#/register |

The organization name determines the `github.io` hostname. Keeping this hostname requires retaining the `review-audit` organization and repository name. This is a static homepage; its login links navigate to Vercel, where the account cookie and API share one origin.

## Recreate or configure Pages

1. Create/select the public `review-audit/review-audit.github.io` repository with `index.html` and `.nojekyll` in the root of `main`.
2. Open **Settings → Pages → Build and deployment**.
3. Set **Source** to **Deploy from a branch**; select **main** and **/ (root)**, then Save.
4. Enable **Enforce HTTPS** if available and not already enabled.
5. Wait until the Pages deployment finishes, then visit the website. No manually authored Actions workflow or external build service is necessary; GitHub manages branch-based Pages publishing.

For an authorized GitHub CLI session, inspect the settings with:

```sh
gh api repos/review-audit/review-audit.github.io/pages
```

Only if Pages is not yet enabled, initialize it with:

```sh
gh api repos/review-audit/review-audit.github.io/pages --method POST \
  -f 'source[branch]=main' -f 'source[path]=/'
```

An already-enabled site returns HTTP 409 for that POST; inspect its existing settings instead of repeatedly creating it.

## Publish changes

1. Edit `index.html` and preview locally:

   ```sh
   python3 -m http.server 8080 --bind 127.0.0.1
   ```

2. Verify the page layout and both destination links. No account data is submitted by this static page.
3. Commit the changes and push `main`. GitHub Pages publishes automatically.
4. Confirm the deployment in **Settings → Pages** or **Actions**, then inspect https://review-audit.github.io/.

If the Vercel application hostname changes, update **both** links in `index.html` and the destinations in this guide. Keep `#/register` on the registration link. No database keys or `.env` file are needed here.

To roll back, revert the relevant homepage commit and push the revert to `main`. This affects only the public homepage; it does not change application accounts or database contents.

## Verify

- The live homepage loads over HTTPS.
- **Sign in** opens the Vercel sign-in form.
- **Create account** opens the Vercel registration tab.
- Backend verification is documented in the private application's `docs/DEPLOYMENT.md` and automated by `npm run verify:deployment -- https://review-audit-seven.vercel.app/` from that repository.

If the homepage returns 404, check the organization/repository spelling, branch source, root `index.html`, and the Pages deployment result. If the homepage works but sign-in fails, inspect the application's Vercel deployment and database configuration rather than the Pages settings.
