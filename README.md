# tracuela.com

The public site: a home page, the privacy policy and the terms of use. Three static files
and one stylesheet — no build step, no dependencies, nothing to run.

It exists because Google will not publish an OAuth app without a home page, and is explicit
that the page may not be hosted "on a third-party platform where you can't verify that you
own your subdomain" — which rules out the `*.expo.app` host the rest of the project uses.
The privacy policy is also what App Store review asks for.

## This directory is the source of truth

The site lives here, in the app repository, and is *pushed* to a separate public repository
for hosting. The app repo is private, and GitHub Pages on a private repo needs a paid plan;
splitting it keeps the source private and the site free to host.

Editing happens here. Publishing is one command:

```sh
git subtree push --prefix site site main
```

where `site` is a remote added once:

```sh
git remote add site git@github.com:rawpaw/tracuela-site.git
```

Never edit the published repo directly — the next subtree push would overwrite it, and the
two copies would disagree in the meantime.

## Hosting

GitHub Pages, serving the published repo's `main` at the root. `CNAME` pins the custom
domain, so the Pages setting and this file must agree.

DNS lives at GoDaddy. The apex needs GitHub's four A records in place of the registrar's
parking records; `www` is a CNAME to the GitHub Pages host. The `clerk`, `accounts` and
`clkmail` records belong to Clerk and must be left alone — changing the apex does not
affect them.

Turn on **Enforce HTTPS** in the Pages settings once the certificate has been issued.
Google requires these URLs over HTTPS and will not accept them otherwise.
