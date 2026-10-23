# Review Audit — public homepage

Live: **https://review-audit.github.io/**

This repository contains the static research-project homepage. Its Sign in and Create account links open the application at **https://review-audit-seven.vercel.app/**. Registration, authentication, reviews and assessments are handled by that application's backend and Turso database, not by GitHub Pages.

Application source (private): [gaojie058/review-audit](https://github.com/gaojie058/review-audit).
Application deployment guide (requires repository access): [docs/DEPLOYMENT.md](https://github.com/gaojie058/review-audit/blob/main/docs/DEPLOYMENT.md).

## Files

- `index.html`: complete responsive homepage, including inline styles and application links.
- `.nojekyll`: tells GitHub Pages to publish the files directly, without Jekyll processing.
- `DEPLOYMENT.md`: exact Pages settings, update steps and verification.

There are no dependencies to install, build commands, environment variables, passwords or database credentials in this repository. Keep all real account data and review data out of it.

To preview locally, run `python3 -m http.server 8080 --bind 127.0.0.1` and open http://127.0.0.1:8080/.
