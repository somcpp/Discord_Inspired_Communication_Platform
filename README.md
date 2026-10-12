**Discord-Inspired Communication Platform**

A lightweight, developer-friendly communication platform inspired by modern real-time chat apps. This repository contains a full-stack Next.js TypeScript application with a separate socket server, realtime messaging, file uploads, and a component-driven UI.

**Project**: A modern web chat platform inspired by popular real-time apps — designed for learning, experimentation, and extension. This project intentionally avoids commercial branding; it focuses on real-time collaboration, modular UI, and a pragmatic architecture.

**Key Features**
- **Real-time messaging:** Text messages, channels, and direct messages with live updates via a dedicated socket server.
- **Servers & channels:** Server (guild)-style grouping, channel lists, and channel creation/editing.
- **Direct messages:** One-to-one conversations with presence indicators.
- **File upload & preview:** Image/file uploads with an upload pipeline.
- **Modals & settings:** Rich modal UX for create/edit/delete flows and server/member management.
- **Emoji & reactions:** Emoji picker and reaction support.
- **Responsive UI:** Desktop and mobile-friendly layout components.
- **Optimistic updates:** Smooth UX with optimistic client-side updates and server reconciliation.

**Architecture Overview**
- Client: Next.js (app directory) + React + TypeScript. UI is split into small, reusable components and provider wrappers for theme, modal, socket, and data fetching.
- API: Next.js API routes under the app/api tree used for REST-style endpoints and server actions.
- Real-time: A separate Node socket server (folder: [socket-server/index.ts](socket-server/index.ts)) handles WebSocket/Socket.IO connections and broadcasts events to clients.
- Database: Prisma is used as the ORM (schema and migrations live under `prisma/`). The code is DB-agnostic — configure your preferred provider in `prisma/schema.prisma`.
- File uploads: Integrated upload handler(s) in `lib/uploadthing.ts` and API routes for upload flow.

**Folder Structure (high level)**
- [app/](app) — Next.js app directory: pages, layouts, and API routes.
- [components/](components) — Reusable UI primitives and domain components (chat, server, modals, navigation, ui).
- [hooks/](hooks) — React hooks used across the app (`use-chat-socket`, `use-modal-store`, etc.).
- [lib/](lib) — Utility helpers, socket emitters, upload helpers, and server helpers.
- [prisma/](prisma) — Prisma schema and migrations.
- [generated/prisma/](generated/prisma) — Generated Prisma client artifacts.
- [socket-server/](socket-server) — Separate realtime server process (socket handling, event routing).

See these folders in the repo root for details: [app/](app), [components/](components), [lib/](lib), [socket-server/](socket-server), [prisma/](prisma).

**Design & Patterns**
- Component-driven UI: Fine-grained components under `components/` keep logic isolated and testable.
- Provider pattern: Global concerns (socket, modal, theme, queries) use React providers in `components/providers/`.
- Separation of concerns: Next.js handles SSR/SSG and API routes, while the socket server handles realtime broadcasts.
- Pragmatic state: Hooks and query-provider patterns reduce prop-drilling and centralize shared state.
- Extensible events: Socket event names and payloads are centralized in `lib/socket.ts` and `lib/socket-emit.ts` for easy extension.

**Tech Stack**
- Framework: `Next.js` (app dir) + `React` + `TypeScript`
- Realtime: Separate Node socket server (Socket.IO or WebSockets) for event distribution
- Database/ORM: `Prisma` (schema in `prisma/`)
- Uploads: Upload utilities under `lib/uploadthing.ts` and API routes for handling file assets
- Styling: Global CSS with PostCSS (see `globals.css` and `postcss.config.mjs`)
- Packaging: `npm` and standard Node tooling

**Local development**
1. Install dependencies:

```bash
npm install
```

2. Configure environment variables: copy and set up `.env` (database URL, upload keys, etc.).

3. Setup database and run migrations (example with Prisma):

```bash
npx prisma migrate dev --name init
npx prisma generate
```

4. Start development servers:

```bash
# Start the Next.js app (root)
npm run dev

# In a second terminal start the socket server
cd socket-server
npm run dev
```

Note: If `package.json` uses different script names, run the relevant scripts shown in that file.

**Environment & Configuration**
- Database connection: configure `DATABASE_URL` in `.env` and update `prisma/schema.prisma` as needed.
- Socket server port and origins: configure in `socket-server/index.ts` and match client socket connection settings in `lib/socket.ts` or provider code.
- Upload credentials: set provider keys for the upload pipeline used by `lib/uploadthing.ts`.

**Testing & Debugging**
- Use Next.js dev server for live-reload front-end debugging.
- Socket server console logs show realtime events; use browser devtools network tab to inspect WebSocket frames.
- Use `npx prisma studio` to inspect DB records during development.

**Contributing**
- New features: fork, branch, and open PRs with focused scope.
- Keep UI changes componentized and add small hooks where shared behavior is required.
- If adding new socket events, update both client emitters (`lib/socket-emit.ts`) and server handlers (`socket-server/index.ts`).

**Roadmap & Ideas**
- Message reactions & threaded replies
- Typing indicators and improved presence
- Message search and pagination
- Richer file preview & CDN-backed uploads
- Server roles, permissions, and audit logs

**Credits & License**
- This repository is for learning and experimentation. Replace with your preferred license in `LICENSE`.

**Need help or want custom changes?**
Open an issue or pull request describing the change. If you want, I can add a README section for deploying to a specific cloud provider or add CI scripts.
# Discord Clone

A full-stack Discord clone built with Next.js, React 19, Socket.io, Prisma, PostgreSQL, Clerk, and LiveKit.

## Getting Started

### 1. Run the Next.js Web Application
```bash
npm run dev
```

### 2. Run the Socket.io Server (in a separate terminal)
```bash
npm run socket
```

## Development Roadmap & Progress
For detailed architectural decisions, phase-by-phase development progress, and upcoming tasks, see [PROGRESS.md](./PROGRESS.md).
