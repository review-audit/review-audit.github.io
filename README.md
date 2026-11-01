# ReviewAudit — public frontend

Live: **https://review-audit.github.io/**

This repository hosts the compiled ReviewAudit web application. Login, registration, the Area Chair Console, review forms and PDF previews stay on `review-audit.github.io`. There is no redirect or embedded Vercel page. The browser calls the Vercel API in the background using the existing account system and database.

Application source (private): [gaojie058/review-audit](https://github.com/gaojie058/review-audit).

## Published files

- `index.html` and `assets/`: compiled React frontend, styles, fonts and PDF worker.
- `.nojekyll`: publish the build directly without Jekyll processing.
- `build-info.json`: the application source commit and public API origin for this release.
- `DEPLOYMENT.md`: release instructions and verification.

Do not edit generated bundles. Build a new release from the private application repository. No passwords, tokens, database credentials, server source or private review data belong here.
