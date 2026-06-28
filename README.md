# iFoto Frontend

Web frontend for the iFoto photography club management system. It provides authentication, role-based access control, and management features for club members, equipment, and events.

## Tech Stack

- **React 19** + **TypeScript** (strict mode), built with **Vite 7**
- **React Router v7** for routing
- **TanStack React Query v5** for server state; **React Context API** for auth state
- **Axios** with custom interceptors (token injection + 401 refresh queue)
- **shadcn/ui** (New York style) + **Radix UI** + **Tailwind CSS v4**
- **Zod 4** for runtime schema validation
- **TanStack React Table v8** for data tables

## Features

- Authentication (login, register, forgot/reset password) with in-memory access tokens and `httpOnly` refresh cookies
- Role-based access control across six roles: `ADMIN`, `CLUB_MEMBER`, `EQUIPMENT_COMMITTEE`, `EVENT_COMMITTEE`, `GUEST`, `HIGH_COMMITTEE`
- Multi-role users with an active-role switcher and role-gated navigation
- User management (list users, edit roles/locked status, delete)
- Equipment and event management modules (in progress)

## Prerequisites

- **Node.js** 18+ and **npm**
- The backend API running on **port 8080** (required for any API calls to succeed)

## Getting Started

1. Install dependencies:

   ```bash
   npm install
   ```

2. (Optional) Configure the API URL. By default the app talks to `http://localhost:8080`. To override, create a `.env` file:

   ```bash
   VITE_API_URL=http://localhost:8080
   ```

3. Start the dev server:

   ```bash
   npm run dev
   ```

   The app runs at [http://localhost:5173](http://localhost:5173) and proxies `/api/*` requests to the backend on port 8080.

## Available Scripts

```bash
npm run dev       # Start the Vite dev server with HMR
npm run build     # Type-check then build for production → /dist
npm run lint      # Run ESLint on all TypeScript files
npm run preview   # Serve the production build locally
```

> No test runner is configured.

## API Conventions

- All endpoints are prefixed with `/api/v1/`.
- Base URL comes from `VITE_API_URL`, defaulting to `http://localhost:8080` in development (also proxied via Vite's `/api` proxy).
- Responses are validated against Zod schemas before reaching components.
- Pagination params: `page` (0-indexed), `size`, `role`, `search`.

## Project Structure

```
src/
├── main.tsx              # App entry: QueryClientProvider + AuthProvider + Router
├── router.tsx            # Route definitions with ProtectedRoute wrappers
├── pages/                # Auth and UserManagement pages
├── store/                # Auth context, query client, query factory, schemas
├── components/           # Layout, sidebar, and shadcn/ui primitives
└── utils/                # Axios instance and helpers
```

## Deployment

A multi-stage `Dockerfile` (nginx) is provided for production builds.
