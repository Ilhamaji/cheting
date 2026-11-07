<div align="center">

# Cheting

A **real-time** full-stack chat app — direct messages, groups, and voice channels. Built with Next.js 15, Prisma, and NextAuth.

[![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)](#)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Prisma](https://img.shields.io/badge/Prisma-5-2D3748?style=flat-square&logo=prisma&logoColor=white)](https://www.prisma.io)

**Demo:** [cheting.vercel.app](https://cheting.vercel.app)

**English** · [Bahasa Indonesia](README.id.md)

</div>

---

## About

Cheting follows the Discord/Slack model: private conversations, groups that contain categories and channels, a friend system, and **WebRTC voice channels**. It started as a portfolio project and as an exploration of real-time architecture on the Next.js App Router.

## Features

### Chat and social

- Register/login through NextAuth, with passwords hashed by `bcryptjs`.
- One-to-one direct messages, plus groups that hold **categories** and **channels**.
- Add friends by email, and online/offline status that updates in real time.
- Profiles with editable avatar and display name.

### Media and voice

- Files upload through `/api/upload` and are served back from `/api/media/[id]`. Images are compressed client-side before sending.
- **Voice channels** run on WebRTC: signalling at `/api/channels/[id]/voice-signals`, participant list at `voice-members`.
- A sound effect plays when a message arrives.

### UI

- Shadcn UI and Radix UI components (Radix handles focus traps and keyboard navigation).
- Page transitions with Framer Motion.
- Dark mode and toast notifications.

## Tech Stack

| Layer | Technology |
| --- | --- |
| Framework | Next.js 15 (App Router) |
| Language | TypeScript |
| Database | PostgreSQL + Prisma ORM |
| Auth | NextAuth.js (Prisma adapter) |
| UI | Shadcn UI + Radix UI |
| Styling | Tailwind CSS |
| Animation | Framer Motion |
| Voice | WebRTC signalling |
| Validation | Zod + React Hook Form |

## Getting Started

### 1. Prerequisites

- Node.js 18+
- A PostgreSQL database
- npm

### 2. Clone and install

```bash
git clone https://github.com/Ilhamaji/cheting.git
cd cheting
npm install
```

### 3. Environment

```env
DATABASE_URL="postgresql://user:pass@localhost:5432/cheting"
NEXTAUTH_SECRET="generate-with: openssl rand -base64 32"
NEXTAUTH_URL="http://localhost:3000"
```

### 4. Set up the database

```bash
npm run db:push       # sync the Prisma schema
npm run db:studio     # (optional) open Prisma Studio
```

### 5. Run

```bash
npm run dev
```

## Scripts

| Command | Purpose |
| --- | --- |
| `npm run dev` | Development server |
| `npm run build` | Prisma generate + production build |
| `npm start` | Serve the production build |
| `npm run lint` | ESLint |
| `npm run db:push` | Sync the schema to the database |
| `npm run db:studio` | Prisma Studio |

## Project Layout

```
app/api/auth/[...nextauth]/           # NextAuth handler
app/api/auth/register/                # manual registration
app/api/messages/                     # send and fetch messages
app/api/friends/                      # friend system
app/api/groups/                       # groups, categories, channels, members
app/api/channels/[id]/voice-signals/  # WebRTC signalling
app/api/channels/[id]/voice-members/  # voice participant list
app/api/media/[id]/                   # media serving
app/api/upload/                       # file upload
app/api/users/profile/                # user profile
app/api/users/status/                 # online status

components/
  chat/chat-sidebar.tsx               # channel and DM list
  chat/chat-window.tsx                # message area
  chat/voice-room.tsx                 # voice channel UI (WebRTC)
  chat/user-avatar.tsx
  providers/session-provider.tsx      # NextAuth session
  providers/theme-provider.tsx
  ui/                                 # Shadcn components (avatar, dialog, ...)

lib/
  auth.ts                             # NextAuth config + bcryptjs
  prisma.ts                           # Prisma client singleton
  socket.ts                           # realtime connection
  security.ts                         # security helpers
  compress-image.ts                   # client-side image compression
  sound.ts                            # incoming-message sound
```

---

<div align="center">
Built by <a href="https://github.com/Ilhamaji">Ilham Aji</a>
</div>
