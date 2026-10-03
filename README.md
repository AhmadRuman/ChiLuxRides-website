# ChiLuxRides — Transportation Booking Website

A portfolio source snapshot of a luxury transportation website for Chicago
and the surrounding suburbs.

## Features

- Responsive React website with fleet, airport, service, and policy pages
- Airport, point-to-point, hourly, and custom-request booking flows
- Itemized fares, payment schedules, child-seat options, and promo codes
- Required agreement to privacy, terms, and cancellation policies
- Stripe-backed deposit and saved-card payment workflows
- Administrative booking, driver, promo-code, and extra-charge controls
- Email notifications through Resend

## Technology

- React, TypeScript, Vite, and Tailwind CSS
- React Hook Form, Zod, and TanStack Query
- Express API server
- PostgreSQL and Drizzle ORM
- OpenAPI-generated API client and validation schemas
- Stripe, Google Maps, and Resend integrations
- pnpm workspace monorepo

## Project layout

```text
artifacts/suv-transport/  Website
artifacts/api-server/     Express API
lib/api-spec/             OpenAPI contract and code generation
lib/api-client-react/     Generated frontend API client
lib/api-zod/              Generated API validation
lib/db/                   Database connection and schema definitions
scripts/                  General workspace scripts
```

## About this public source copy

This is a separately prepared copy, not an export of the production database.
It does not contain credentials, Git history, customer bookings, database
backups, workspace notes, raw uploads, or build output.

The business branding, public website addresses, public contact information,
pricing rules, and public website images are intentionally retained.
Database schema definitions describe the application structure; they are not
customer records.

Differences from the working project:

- Customer-review seed data has been replaced with a clearly labeled synthetic example.
- Original analytics IDs and site-verification files/tokens have been removed.
- Image EXIF/XMP/IPTC and text/comment metadata has been removed where supported.
- The exported admin code requires an explicitly configured session secret;
  its development fallback was removed.
- Replit workspace/deployment metadata and the design mockup sandbox are excluded.

The original working website was not modified.

## Setup expectations

Use a current Node.js release and pnpm. Install dependencies with:

```sh
pnpm install --frozen-lockfile
```

See `.env.example` for variable names. Its values are intentionally blank.
Configure your own credentials privately; never commit a filled-in environment
file. This example file is documentation, not an automatic secrets loader for
all workspace packages.

The original application uses Replit-managed routing and integrations. For a
new Replit project, recreate the API routing, PostgreSQL database, environment
configuration, and Stripe/Resend connections. Outside Replit, adapt the
connector-backed email client and configure an API reverse proxy.

On a **new, empty development database**, the schema can be applied with:

```sh
pnpm --filter @workspace/db run push
```

Do not run this command against an existing or production database without
reviewing the proposed changes.

Useful commands:

```sh
# Refresh generated API schemas/client after changing the OpenAPI contract
pnpm --filter @workspace/api-spec run codegen

# Check shared-library types
pnpm run typecheck:libs

# API process, after configuring its database and secrets
PORT=8080 pnpm --filter @workspace/api-server run dev

# Website development process
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/suv-transport run dev

# Website production build
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/suv-transport run build
```

For local end-to-end use, route `/api` from the frontend origin to the Express
process. Starting the two processes alone does not create that routing.
Mail and payments need your own integrations; use test-mode credentials and
synthetic customer data while evaluating the project.

This is a full-stack application, not a standalone GitHub Pages site.

## Uploading the showcase to GitHub

1. Extract the ZIP and open the `chiluxrides-github-showcase` folder.
2. Create a new **private** GitHub repository.
3. Upload the extracted folder's contents, including `.gitignore` and
   `.env.example`. GitHub Desktop is convenient for uploading the full folder;
   browser uploads may need smaller batches because of file-count limits.
   Do not upload the ZIP itself as the source repository.
4. Review the files on GitHub, particularly any files you add afterward.
5. Make the repository public only when satisfied with that review.

Alternatively, initialize a fresh Git repository in the extracted folder:

```sh
git init
git add .
git status
git commit -m "Add transportation website portfolio source"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

Only substitute your public GitHub username and repository name in that URL.
Authenticate through GitHub's normal tools; do not put an access token in
the URL or project files.

## Security and limitations

Read `PUBLICATION_REVIEW.md` before deploying this copy.
Secret-pattern scanning found no embedded credentials in the packaged source.
That is not a guarantee against every possible secret, nor a production
security certification.

A separate project-wide dependency audit reported vulnerable dependencies.
These were not upgraded as part of preparing this source ZIP. Review and
remediate them before deploying a new instance.

The original full frontend typecheck also has three existing errors involving
vehicle-category types and an SEO component property. Preparing this copy did
not fix unrelated application issues.

## Image and brand rights

Images and branding are included to show the original project. Their presence
does not grant permission to reuse third-party content or trademarks.