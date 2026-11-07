<div align="center">

# Chetting

Aplikasi chat full-stack **real-time** — DM, grup, dan voice channel. Dibangun dengan Next.js 15, Prisma, dan NextAuth.

[![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)](#)
[![Next.js](https://img.shields.io/badge/Next.js-15-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Prisma](https://img.shields.io/badge/Prisma-5-2D3748?style=flat-square&logo=prisma&logoColor=white)](https://www.prisma.io)

**Demo:** [chetting-xi.vercel.app](https://chetting-xi.vercel.app)

<!-- lang-switcher -->
[English](README.md) · **Bahasa Indonesia**

</div>

---

## Tentang

Chetting adalah aplikasi chat ala Discord/Slack: percakapan pribadi, grup dengan kategori dan channel, sistem pertemanan, serta **voice channel** berbasis WebRTC. Dibangun sebagai project portfolio sekaligus eksplorasi arsitektur real-time di Next.js App Router.

## Fitur

### Chat & Sosial

- Register/login lewat NextAuth; password di-hash dengan `bcryptjs`.
- DM satu-lawan-satu, plus grup yang punya **kategori** dan **channel** di dalamnya.
- Tambah teman lewat email, dan status online/offline yang di-update real-time.
- Profil dengan avatar dan display name yang bisa diubah.

### Media & Voice

- Upload file lewat `/api/upload`, disajikan kembali dari `/api/media/[id]`. Gambar dikompresi di klien sebelum dikirim.
- **Voice channel** memakai WebRTC: signalling di `/api/channels/[id]/voice-signals`, daftar anggota di `voice-members`.
- Efek suara saat pesan masuk.

### UI

- Komponen dari Shadcn UI + Radix UI (focus trap dan keyboard nav ditangani Radix).
- Transisi antar-halaman dengan Framer Motion.
- Dark mode dan toast notification.

## Tech Stack

| Bagian | Teknologi |
| --- | --- |
| Framework | Next.js 15 (App Router) |
| Bahasa | TypeScript |
| Database | PostgreSQL + Prisma ORM |
| Auth | NextAuth.js (Prisma adapter) |
| UI | Shadcn UI + Radix UI |
| Styling | Tailwind CSS |
| Animasi | Framer Motion |
| Voice | WebRTC signalling |
| Validasi | Zod + React Hook Form |

## Menjalankan

### 1. Prasyarat

- Node.js 18+
- Database PostgreSQL
- npm

### 2. Clone & install

```bash
git clone https://github.com/Ilhamaji/chetting.git
cd chetting
npm install
```

### 3. Environment

```env
DATABASE_URL="postgresql://user:pass@localhost:5432/chetting"
NEXTAUTH_SECRET="generate-with: openssl rand -base64 32"
NEXTAUTH_URL="http://localhost:3000"
```

### 4. Setup database

```bash
npm run db:push       # sinkronkan schema Prisma
npm run db:studio     # (opsional) buka Prisma Studio
```

### 5. Jalankan

```bash
npm run dev
```

## Scripts

| Command | Kegunaan |
| --- | --- |
| `npm run dev` | Development server |
| `npm run build` | Prisma generate + build produksi |
| `npm start` | Jalankan hasil build |
| `npm run lint` | ESLint |
| `npm run db:push` | Sinkronkan schema ke database |
| `npm run db:studio` | Prisma Studio |

## Struktur

```
app/api/auth/[...nextauth]/           # NextAuth handler
app/api/auth/register/                # registrasi manual
app/api/messages/                     # kirim & ambil pesan
app/api/friends/                      # sistem pertemanan
app/api/groups/                       # grup, kategori, channel, anggota
app/api/channels/[id]/voice-signals/  # signalling WebRTC
app/api/channels/[id]/voice-members/  # daftar anggota voice
app/api/media/[id]/                   # penyajian media
app/api/upload/                       # unggah file
app/api/users/profile/                # profil pengguna
app/api/users/status/                 # status online

components/
  chat/chat-sidebar.tsx               # daftar channel & DM
  chat/chat-window.tsx                # area pesan
  chat/voice-room.tsx                 # UI voice channel (WebRTC)
  chat/user-avatar.tsx
  providers/session-provider.tsx      # NextAuth session
  providers/theme-provider.tsx
  ui/                                 # komponen Shadcn (avatar, dialog, ...)

lib/
  auth.ts                             # konfigurasi NextAuth + bcryptjs
  prisma.ts                           # Prisma client singleton
  socket.ts                           # koneksi realtime
  security.ts                         # helper keamanan
  compress-image.ts                   # kompresi gambar sisi klien
  sound.ts                            # efek suara pesan masuk
```

---

<div align="center">
Dibuat oleh <a href="https://github.com/Ilhamaji">Ilham Aji</a>
</div>
