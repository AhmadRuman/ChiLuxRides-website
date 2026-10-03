# ChiLuxRides

### Luxury Transportation Website & Booking Platform

A full-stack transportation booking website for Chicago and the surrounding suburbs. The project combines a responsive customer-facing website with fare calculation, booking requests, payment processing, and administrative tools.

## Features

### Customer Experience

- Responsive layouts for desktop, tablet, and mobile
- Fleet, airport, service-area, and policy pages
- Airport, point-to-point, hourly, and custom-request booking flows
- Itemized fare breakdowns and deposit payment schedules
- Child-seat options and promotional codes
- Required agreement to privacy, terms, and cancellation policies

### Payments & Notifications

- Stripe-backed deposits and saved-card payment workflows
- Remaining-balance and additional-charge management
- Booking email notifications through Resend
- Google Maps integration for address and route-related functionality

### Administration

- Administrative sign-in
- Booking review and management
- Driver assignment and management
- Promotional-code management
- Additional-charge controls

## Technology Stack

| Layer | Technologies |
| --- | --- |
| Frontend | React, TypeScript, Vite, Tailwind CSS |
| Forms & validation | React Hook Form, Zod |
| API state | TanStack Query |
| Backend | Node.js, Express |
| Database | PostgreSQL, Drizzle ORM |
| API contract | OpenAPI with generated clients and validation schemas |
| Integrations | Stripe, Google Maps, Resend |
| Workspace | pnpm monorepo |

## Project Structure

```text
artifacts/
  suv-transport/        React website
  api-server/           Express API
lib/
  api-spec/             OpenAPI contract and code generation
  api-client-react/     Generated frontend API client
  api-zod/              Generated API validation schemas
  db/                   Database connection and schema definitions
scripts/                Workspace utilities
```

## Getting Started

### Prerequisites

- A current Node.js release and pnpm
- A PostgreSQL development database
- Your own credentials for the integrations you want to use
- A routing configuration that forwards `/api` requests to the Express server

### Install Dependencies

From the repository root:

```sh
pnpm install --frozen-lockfile
```

### Configure the Environment

Use `.env.example` as a reference for the required environment-variable names. Supply values through private environment configuration; do not commit credentials.

The example file does not automatically load configuration into every workspace package. Make the required variables available to each process before starting it.

The application was developed with Replit-managed routing and integrations. When running it elsewhere, configure an API reverse proxy and adapt the connector-backed email integration to your environment.

### Initialize a Development Database

Apply the schema only to a **new, empty development database**:

```sh
pnpm --filter @workspace/db run push
```

Review proposed schema changes before using this command with an existing database. Do not apply development commands directly to production.

### Start the Application

Run the API server:

```sh
PORT=8080 pnpm --filter @workspace/api-server run dev
```

In a separate terminal, start the website:

```sh
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/suv-transport run dev
```

These examples use Unix-style environment-variable syntax.

For end-to-end functionality, configure `/api` on the frontend origin to forward to the API server. Starting both processes does not automatically establish that routing.

## Development Commands

```sh
# Regenerate API clients and validation schemas after contract changes
pnpm --filter @workspace/api-spec run codegen

# Type-check shared libraries
pnpm run typecheck:libs

# Type-check the frontend
pnpm --filter @workspace/suv-transport run typecheck

# Build the website for production
PORT=5173 BASE_PATH=/ pnpm --filter @workspace/suv-transport run build
```

## Project Status

This repository is a portfolio version of the application. Payment, mapping, and email features require separately configured service accounts.

The website production build succeeds. The full frontend typecheck currently reports existing vehicle-category and SEO-property typing issues.

This is a full-stack application, not a standalone static site for GitHub Pages. Deploying it requires a frontend, API server, database, and integration configuration.

## Security & Development Practices

- Keep API secrets, database credentials, and administrator credentials outside version control.
- Use Stripe test mode and fictional customer information during development.
- Seeded testimonial content in this repository is demonstration data.
- Review dependencies, access controls, API-key restrictions, and deployment settings before production use.

## Branding & Assets

Branding and images are included to demonstrate the project. Their inclusion does not grant permission to reuse third-party content or trademarks.
