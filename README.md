# Review Audit — sign-in entry

Live: **https://review-audit.github.io/**

This repository provides the public entry to ReviewAudit. Visiting the homepage automatically opens the application’s sign-in page at **https://review-audit-seven.vercel.app/#/login**. The page uses an immediate redirect with a no-JavaScript meta-refresh fallback and visible sign-in / registration links. Registration, authentication, reviews and assessments are handled by that application's backend and Turso database, not by GitHub Pages.

Application source (private): [gaojie058/review-audit](https://github.com/gaojie058/review-audit).
Application deployment guide (requires repository access): [docs/DEPLOYMENT.md](https://github.com/gaojie058/review-audit/blob/main/docs/DEPLOYMENT.md).

## Files

- `index.html`: sign-in redirect with responsive fallback content and application links.
- `.nojekyll`: tells GitHub Pages to publish the files directly, without Jekyll processing.
- `DEPLOYMENT.md`: exact Pages settings, update steps and verification.

There are no dependencies to install, build commands, environment variables, passwords or database credentials in this repository. Keep all real account data and review data out of it.

To preview locally, run `python3 -m http.server 8080 --bind 127.0.0.1` and open http://127.0.0.1:8080/.
