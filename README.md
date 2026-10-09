# Folivio

**Your world of investing.** Android-first Expo / React Native / TypeScript research and paper trading across **NEPSE, US Stocks, and India**. iOS-compatible source and a web development preview are included.

This is a functioning development application, with persistent demo accounts, navigation, search, watchlists, instrument charts, virtual orders, receipts, portfolios, themes, and identity test fixtures. Supabase adapters, PostgreSQL migrations/RLS, secure Auth flows, private identity storage, and protected reviewer/retention endpoints are implemented. Production services require configuration and integration testing.

**Folivio Admin** is the independent Next.js application in `apps/admin`, with eleven operational modules, five server-enforced roles, MFA-gated access, private KYC review, support conversations, content publication and audited interventions. The latest visual revision uses forest green and warm ivory, with lime, copper and sage accents in both applications. Admin source and SQL are implemented; its full Next.js build and hosted service flows remain unverified because this environment could not install the required packages or access the local preview port. See [admin validation](docs/ADMIN_VALIDATION.md).

Open the delivered `../folivio-admin-design.html` for a portable **read-only** review of all eleven sections and both themes. For a functioning synthetic local admin demo, install root dependencies and run `npm run preview:admin`; for the Next application, follow [admin setup](docs/ADMIN_SETUP.md). Local mobile and admin fixtures are independent; hosted mode connects both applications to the same Supabase project.

**V1 never routes real securities orders, accepts deposits, or exchanges currencies.** Foreign-market research does not imply legal permission to invest from Nepal. Every supplied quote and chart is explicitly fictional. The refreshed interface uses the supplied Binance and TradingView screenshots for layout inspiration, with original Folivio branding and explicitly labeled sample graphics.

## Run the local demo

Node 24 LTS and npm are recommended. From this directory:

```powershell
npm ci
Copy-Item .env.example .env
npm start
```

Open the project in a compatible Expo development build, or use `npm run web` for the browser preview. Select **Explore the working demo** on the welcome screen. No account, credentials, email delivery, SMS, or network market feed is needed. `.env` defaults to `EXPO_PUBLIC_APP_MODE=demo`; the application does not initialize a Supabase client in this mode.

Initial virtual balances are **NPR 1,000,000**, **USD 10,000**, and **INR 500,000**. Trades, watchlists, theme, and selected market survive navigation and restart. Virtual transactions use whole shares and fixed samples, with no fees or currency conversion. Clearing application data clears demo activity. Logging out clears the local session; it intentionally retains demo orders for a later demo visit.

## Validate

```powershell
npm run check
npx expo-doctor
npm run export:web
npx expo export --platform android --output-dir work/android-export
npx expo export --platform ios --output-dir work/ios-export
```

`npm test` executes unit/service tests and the **actual SQL migrations in embedded PostgreSQL (PGlite)**, including role grants, RLS, transactional fills, idempotency, contact restrictions, private storage policies, and KYC transitions. It does not require Docker. For a running local Supabase stack, `npm run test:database` also runs pgTAP tests. See [validation evidence](docs/VALIDATION.md) for the commands actually run and limits of the evidence.

## Documentation

- [Configure Supabase, email, SMS, and callbacks](docs/SETUP.md)
- [Android/iOS development and production build preparation](docs/ANDROID.md)
- [Identity review, private storage, retention, and deletion](docs/KYC.md)
- [Architecture and provider contracts](docs/ARCHITECTURE.md)
- [Market-data candidates and licensing research](docs/MARKET_DATA.md)
- [Security boundaries and remaining release requirements](docs/SECURITY.md)
- [Testing and validation evidence](docs/VALIDATION.md)
- [Interface refresh and graphic definitions](docs/UI_REDESIGN.md)
- [Administrator setup, roles and workflows](docs/ADMIN_SETUP.md)
- [Independent admin deployment and mobile synchronization](docs/ADMIN_DEPLOYMENT.md)
- [Admin test results and remaining verification](docs/ADMIN_VALIDATION.md)

## Project map

```text
app/                     Expo Router routes, authentication and app layouts
apps/admin/              Independent Next.js dashboard, server routes and component system
packages/                Shared admin contracts, validation, push contract and synthetic SQL fixtures
components/              Accessible UI, charts, logo, market header
features/                Auth, onboarding, verification, research, trading, portfolio, profile
services/auth/           Supabase Auth, secure storage, session and biometric lifecycle
services/market-data/    Provider interfaces, fictional samples, Supabase sample adapter
services/paper-trading/  Execution contract, local engine, backend RPC adapter
services/kyc/            Field validation, state machine, private submission adapter
state/                   Zustand preferences, session state and local demo ledger
hooks/                   TanStack Query, action/error handling, cooldowns
theme/                   Dark/light tokens and system-mode resolution
types/                   Domain contracts
assets/                  Original icon, adaptive icon, splash and SVG concept
supabase/migrations/     Schema, grants, RLS, transactional execution and KYC workflow
supabase/functions/      MFA-checked reviewer, protected retention and authenticated paper-order APIs
tests/                   Unit, service, persistence and PostgreSQL tests
docs/                    Setup, security, architecture and release notes
```

## What remains external

A Supabase project, SMTP sender, supported SMS provider with Nepal delivery capability, approved identity-review operation and retention schedule, market-data display rights, physical Android/iPhone testing, EAS credentials, signing identities, operator terms/support, and regulatory review. None is silently simulated as a configured production service. No API secret, service-role key, real identity document, or credential is included.
