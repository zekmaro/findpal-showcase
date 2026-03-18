# FindPal

> **Stop swiping. Start doing.**

FindPal is a social app for meeting people through shared activities. Think Meetup, but for small groups, casual vibe, and 18–30 year olds who want real connections without the pressure of dating apps.

🌐 **[findpal.app](https://findpal.app)**

---

## The Problem

- Young people in cities are lonely but won't admit it
- Dating apps feel transactional and exhausting
- Making friends after university is weirdly hard
- Nobody wants to show up to a 200-person corporate meetup

## The Solution

An app where the **event is the excuse** — the real product is connection without pressure.

- 🎯 **Activity-first** — not looks-first like dating apps
- 👥 **Small groups** — 3–10 people, not massive meetups
- 🚀 **Solo-friendly** — designed for showing up alone
- 🎲 **Low commitment** — one-off events, not group memberships

---

## Screenshots

<!-- Add screenshots here -->
| Discover | Event Detail | Search |
|----------|-------------|--------|
| ![Discover](screenshots/discover.png) | ![Event](screenshots/event.png) | ![Search](screenshots/search.png) |

---

## Features

**For users**
- Swipe-based event discovery (Tinder-style)
- Full search with category, language, and sort filters
- Join events and chat with attendees in real time
- Follow other users, get notified when they post events
- Share events via link with web preview + OG metadata
- Public profiles with interests, bio, and follower counts
- Forgot password flow with email reset

**For hosts**
- Create events with cover photo, date, location, tags
- Cancel, restore, or archive events
- See who's joining

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Mobile App | React Native + Expo |
| API | Express.js + TypeScript |
| Database | PostgreSQL + Prisma ORM |
| Auth | JWT (access + refresh tokens) |
| Image Storage | Cloudinary |
| Email | Resend |
| Landing Page | Next.js 14 + Tailwind CSS |
| Backend Hosting | Railway |
| Frontend Hosting | Vercel |

---

## Architecture

```
findpal/
├── backend/          # Express.js REST API
│   ├── src/routes/   # Auth, events, chat, notifications, follow...
│   ├── src/services/ # Business logic
│   └── prisma/       # PostgreSQL schema + migrations
│
├── frontend/         # React Native (Expo)
│   ├── src/screens/  # All app screens
│   ├── src/hooks/    # Custom hooks (events, user, push notifications)
│   ├── src/api/      # API client functions
│   └── src/auth/     # JWT auth context
│
└── landing/          # Next.js landing page + event web previews
    └── app/
        ├── page.tsx          # Main landing page
        └── event/[id]/       # Dynamic event preview pages
```

**Key design decisions:**
- Cursor-based pagination for infinite scroll
- Soft delete on users and events
- JWT access tokens (15min) + refresh tokens (7 days)
- Route → Service pattern on the backend
- Push notifications via Expo + FCM/APNs

---

## API Highlights

```
POST   /auth/register          # 4-step onboarding
POST   /auth/login
POST   /auth/forgot-password   # Resend email flow
POST   /auth/reset-password

GET    /event/events            # Paginated feed
GET    /event/search            # Full-text search + filters
POST   /event/create
PATCH  /event/:id/edit
POST   /event/:id/join
POST   /event/:id/leave

GET    /chat/event/:id          # Per-event chat rooms
POST   /chat/:id/messages

POST   /follow/:id              # Follow system
GET    /notification            # In-app + push notifications
```

---

## Running Locally

**Prerequisites:** Docker, Node.js 18+

```bash
# Start database
make upd

# Backend
cd backend && npm install && npm run dev

# Frontend
cd frontend && npm install && npx expo start

# Landing page
cd landing && npm install && npm run dev
```

---

## Status

Currently in **beta** — live at [findpal.app](https://findpal.app), targeting Vienna as the launch city.

---

*Built by [@zekmaro](https://github.com/zekmaro)*
