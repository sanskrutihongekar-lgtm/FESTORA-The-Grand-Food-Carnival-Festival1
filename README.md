# FESTORA 2027 – Event Management Platform

Complete event website + administration dashboard for **FESTORA – The Grand Food & Carnival Festival** (12–15 January 2027, Belagavi).

Built for college students who need to deploy without using a terminal.

---

## What is included (Foundation)

- Next.js (App Router) + TypeScript + Tailwind CSS
- Full Prisma schema for Neon PostgreSQL (users, roles, events, registrations, tickets, QR, SPOCs, stalls, speakers, emails, reminders, audit logs, etc.)
- Authentication (JWT cookie sessions) + role-based access control skeleton
- Seed data pre-filled with FESTORA 2027 details + Super Admin account
- Public home page with festival branding
- Environment variable template
- Vercel configuration
- Student-friendly deployment path (GitHub web upload → Vercel)

**Still to be expanded in next iterations:** full registration form engine, ticket + QR generation API, scanner UI, complete admin CRUD modules, Resend email flows, SPOC assignment UI, dynamic page content editor.

---

## Student deployment steps (no terminal required)

### 1. Download & extract
Download the project ZIP and extract it on your computer.

### 2. Create a GitHub repository
1. Go to [github.com](https://github.com) and sign in.
2. Click **New repository**.
3. Name it e.g. `festora-2027`.
4. Leave it empty (no README).
5. Click **Create repository**.

### 3. Upload the files
1. On the empty repository page click **uploading an existing file**.
2. Drag **all** the folders and files from the extracted project into the browser.
3. Commit the changes.

### 4. Deploy on Vercel
1. Go to [vercel.com](https://vercel.com) and sign in with GitHub.
2. Click **Add New… → Project**.
3. Import the GitHub repository you just created.
4. Leave the default settings (Framework: Next.js).
5. **Before deploying**, open **Environment Variables** and add the required ones (see below).
6. Click **Deploy**.

### 5. Required environment variables

| Variable | Required? | How to get it |
|----------|-----------|---------------|
| `DATABASE_URL` | Yes | Create a free project at [neon.tech](https://neon.tech) → copy the connection string |
| `AUTH_SECRET` | Yes | Any long random string (min 32 characters) |
| `NEXT_PUBLIC_APP_URL` | Yes | Your Vercel URL, e.g. `https://festora-2027.vercel.app` |
| `RESEND_API_KEY` | For emails | [resend.com](https://resend.com) → API Keys |
| `RESEND_FROM_EMAIL` | For emails | A verified sender on Resend |
| `RESEND_FROM_NAME` | Optional | e.g. `FESTORA 2027` |

After the first successful deploy you still need to push the database schema and seed data. Because students cannot run terminal commands, a one-time browser setup page will be added in the next version. For now, a developer can run:

```
npx prisma db push
npx tsx prisma/seed.ts
```

### 6. First login
- URL: `https://your-app.vercel.app/admin`
- Email: `admin@festora.in`
- Password: `FestoraAdmin2027!`

**Change this password immediately.**

---

## Local development (for developers only)

```bash
npm install
cp .env.example .env
# fill DATABASE_URL and AUTH_SECRET
npx prisma db push
npx tsx prisma/seed.ts
npm run dev
```

---

## Project structure (foundation)

```
festora-platform/
├── prisma/
│   ├── schema.prisma      # Full database schema
│   └── seed.ts            # FESTORA data + Super Admin
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx       # Public home
│   │   └── api/           # API routes (to be expanded)
│   ├── lib/
│   │   ├── prisma.ts
│   │   └── auth.ts        # Session + password helpers
│   └── components/
├── .env.example
├── vercel.json
├── package.json
└── README.md
```

---

## Next steps for the complete platform

1. Registration API + dynamic form renderer
2. Ticket generation + QR code + verification endpoint
3. Admin dashboard layout + CRUD for Event, Ticket Types, Registrations
4. SPOC management and automatic assignment on tickets
5. Resend integration + email templates
7. Check-in scanner page (mobile-friendly)
8. One-click database setup page for pure student flow

---

Built for FESTORA 2027 · Belagavi
