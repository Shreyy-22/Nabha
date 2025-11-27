**Project Overview**

- **Name:** Nabha — Telemedicine Next.js app
- **Purpose:** A small telemedicine frontend/backend app built with Next.js (App Router), TypeScript, Tailwind CSS and MongoDB that demonstrates authentication, chat, appointments, and basic record management.

**Quick Start**

- **Prerequisites:** Node.js (v18+ recommended), npm or pnpm, a MongoDB instance.
- **Install:**

```powershell
cd Nabha
npm install
```

- **Run (dev):**

```powershell
npm run dev
```

- **Build & start (production):**

```powershell
npm run build
npm start
```

**Important Scripts**

- **`dev`:** runs Next.js in development mode.
- **`build`:** builds the production application.
- **`start`:** starts the production server after `build`.

Check `package.json` for the exact script names.

**Environment**

- **`MONGODB_URI`**: Connection string for MongoDB.
- **`NEXTAUTH_URL`** (if applicable): Base URL for auth/session handling.
- Add other secrets to `.env.local` at the project root.

**Architecture & Key Files**

- **Framework:** Next.js (App Router) + TypeScript.
- **Styling:** Tailwind CSS (see `tailwind.config.ts`).
- **Pages & API:** App routes live in `src/app/` using the App Router; server routes are under `src/app/api/`.

- **Major folders:**
  - `src/app/` : App pages, layouts and API routes.
  - `src/components/` : Reusable UI components and layouts.
  - `src/contexts/` : React contexts (Auth, Language).
  - `src/lib/` : Utilities, auth helpers and MongoDB connection (`mongodb.ts`).
  - `src/models/` : Mongoose or model definitions (e.g., `User.ts`).
  - `src/i18n/` : Localization helpers and routing for messages.
  - `src/types/` : Shared TypeScript types.

**Tech Stack**

- **Frontend / Framework:** Next.js (App Router) + React + TypeScript
- **Styling:** Tailwind CSS
- **State & Context:** React Contexts (`AuthContext`, `LanguageContext`)
- **Database:** MongoDB (access via `src/lib/mongodb.ts`)
- **API:** Next.js server routes in the App Router (`src/app/api/*/route.ts`)
- **Validation & Models:** TypeScript types in `src/types/` and models in `src/models/`
- **i18n:** Simple JSON-based messages in `public/messages/`

**Architecture Diagram (Mermaid)**

Below is a high-level architecture diagram that shows how the main parts of the project interact. You can preview this Mermaid diagram with a Mermaid extension in your editor or on Mermaid live editors.

```mermaid
flowchart LR
  subgraph Client
    Browser[Browser / User]
  end

  subgraph App[Next.js App (src/app)]
    Pages[Pages & Layouts]
    Components[UI Components]
    Contexts[Auth & Language Contexts]
    ApiLayer[Server API Routes `src/app/api/*`]
  end

  subgraph ServerLib[Server Helpers]
    AuthLib[`src/lib/auth.ts`]
    MongoLib[`src/lib/mongodb.ts`]
    Validations[`src/lib/validations/*`]
  end

  subgraph DB[MongoDB]
    Database[(MongoDB Atlas / Self-hosted)]
  end

  subgraph Public[Static / i18n]
    Messages[`public/messages/*.json`]
  end

  Browser --> Pages
  Pages --> Components
  Pages --> Contexts
  Pages --> ApiLayer

  ApiLayer --> AuthLib
  ApiLayer --> MongoLib
  ApiLayer --> Validations

  AuthLib --> Database
  MongoLib --> Database
  Messages --> Pages

  Components --> Contexts
  Contexts --> AuthLib

  style App fill:#f8fafc,stroke:#cbd5e1
  style ServerLib fill:#fff7ed,stroke:#f59e0b
  style DB fill:#ecfccb,stroke:#84cc16
  style Public fill:#eef2ff,stroke:#60a5fa
  style Client fill:#ffffff,stroke:#94a3b8
``` 

**Notable Pages & API Routes**

- `src/app/page.tsx` — Home / landing page.
- `src/app/login/page.tsx`, `src/app/signup/page.tsx` — Auth UI.
- `src/app/appointments/page.tsx` — Appointments list/booking.
- `src/app/profile/page.tsx` — User profile.
- `src/app/api/auth/*/route.ts` — Authentication routes: `login`, `logout`, `signup`, `session`.
- `src/app/api/chat/route.ts` — Chat endpoint.

**Auth & Session**

- Authentication is handled via server API routes in `src/app/api/auth` and helpers in `src/lib/auth.ts`.
- User model is in `src/models/User.ts` and validations for auth are in `src/lib/validations/auth.ts`.

**Database**

- `src/lib/mongodb.ts` manages the MongoDB connection pooling for server-side code.
- Provide `MONGODB_URI` in `.env.local` and ensure the database is reachable before running the app.

**Localization**

- Translations live in `public/messages/` (e.g., `en.json`, `hi.json`, `pa.json`).
- Language selection is managed by `src/contexts/LanguageContext.tsx` and `src/components/LanguageSwitcher.tsx`.

**Development Notes**

- Use the `AuthContext` (`src/contexts/AuthContext.tsx`) for client-side auth state.
- UI primitives are under `src/components/ui/` (e.g., `Button.tsx`, `Input.tsx`, `Card.tsx`).
- Keep route logic in `src/app/api/*/route.ts` to leverage server-side advantages.

**Testing & Linting**

- This repository includes ESLint configuration (`eslint.config.mjs`) and TypeScript setup (`tsconfig.json`). Run your linter and type checks before PRs:

```powershell
npm run lint
npm run type-check
```

**Contributing**

- **Fork & Branch:** Create a feature branch per change.
- **Format & Lint:** Run linters/formatters and add tests where appropriate.
- **Describe Changes:** Keep PR descriptions concise and reference related issues.

**Next Steps / TODOs**

- Add a `README` badge for CI and coverage if you add tests.
- Add example `.env.local.example` listing required environment variables.

**Contact**

- For questions about the code, reach the original author or open an issue in the repository.
