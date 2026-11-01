# Deploy the GitHub Pages frontend

| Setting | Value |
| --- | --- |
| Repository | `review-audit/review-audit.github.io` |
| Pages source | Deploy from a branch: `main` / root |
| HTTPS | Enforced |
| Custom domain | None |
| Frontend | https://review-audit.github.io/ |
| API | https://review-audit-seven.vercel.app/api |

The full frontend is served by GitHub Pages. Application navigation uses hash routes, such as `#/login`, `#/register`, `#/papers` and `#/reviews/…`. Do not replace the frontend with a redirect or an iframe.

## Publish a release

1. In the private application repository, run `npm run check`, commit, and push `main`. Wait for the matching Vercel production deployment to be ready.
2. Update this Pages checkout, then run from the application repository:

   ```sh
   node scripts/publish-pages.mjs /path/to/review-audit.github.io
   ```

   The script builds the Pages version, copies browser assets, and records the source SHA in `build-info.json`. It requires a clean application checkout and verifies the destination repository. Older hashed assets are kept for open browser tabs.
3. Review the generated diff, commit and push this repository's `main` branch. GitHub Pages publishes automatically.
4. Check **Actions → pages build and deployment** and confirm that it succeeded for the new commit.
5. Visit https://review-audit.github.io/#/login and verify that the address stays on this domain when switching to registration and navigating the application.

If the API hostname changes, update the Pages build target and publishing script in the private source repository, rebuild, and republish. No API secrets are needed for this static build.

## Authentication and data

Vercel continues to run the API and use the existing database. Its CORS allowlist explicitly includes only this public frontend origin. The Pages frontend uses a short-lived opaque session token in tab-scoped session storage and sends it in the API Authorization header. No token is added to navigation URLs or external PDF requests. Third-party cookies are not required. Reloading a signed-in tab preserves its session; an independent new tab may require signing in again.

The Vercel frontend remains compatible with its existing HttpOnly cookie sessions. Account passwords and review data are shared across the two frontends. Workspace ownership and version checks still run on the backend.

## Verify and roll back

- Confirm `build-info.json` contains the intended application SHA.
- Verify login, registration navigation, console, review forms, authenticated PDF preview and logout without a domain change.
- Check the browser console for failed API requests or CORS errors.
- Confirm requests from other origins are rejected and unauthenticated review requests return 401.
- Revert a Pages release commit to restore the previous frontend. Revert the backend separately only when compatible with the frontend and database schema.

Application operations: [private deployment guide](https://github.com/gaojie058/review-audit/blob/main/docs/DEPLOYMENT.md).
