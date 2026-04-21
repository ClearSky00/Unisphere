# Unisphere

A full-stack tutoring marketplace that connects students with tutors for live video sessions. Built with Next.js 15, Supabase, Agora, and Stripe.

## Features

- **Tutor Marketplace** — Browse and filter tutors by subject, availability, and rating
- **Session Booking** — Request, accept, and schedule tutoring sessions
- **Live Video Calls** — Real-time video/audio via Agora RTC with screen sharing
- **Payments** — Session credits purchased via Stripe
- **Dashboard** — Separate tutor and student views for managing sessions
- **Admin Panel** — Review and approve tutor applications
- **Resources** — Shared study materials between tutors and students
- **Authentication** — Email/password and Google OAuth via Supabase Auth

## Tech Stack

| Layer | Tech |
|-------|------|
| Framework | Next.js 15 (App Router) |
| Language | TypeScript |
| Database & Auth | Supabase |
| Video | Agora RTC |
| Payments | Stripe |
| UI | shadcn/ui + Tailwind CSS + Radix UI |
| Forms | React Hook Form + Zod |
| Data Fetching | TanStack Query |

## Getting Started

### Prerequisites

- Node.js 18+
- A Supabase project
- An Agora account
- A Stripe account

### Environment Variables

Create a `.env.local` file in the root with:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Agora
NEXT_PUBLIC_AGORA_APP_ID=your-agora-app-id
AGORA_APP_ID=your-agora-app-id
AGORA_APP_CERTIFICATE=your-agora-app-certificate

# Stripe
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your-stripe-publishable-key
STRIPE_SECRET_KEY=your-stripe-secret-key
STRIPE_WEBHOOK_SECRET=your-stripe-webhook-secret
```

### Installation

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Production Build

The production build automatically strips all console statements:

```bash
npm run build:production
```

Or manually:

```bash
# Remove console logs then build
./build-production.sh

# Remove console logs only
./remove_console_logs.sh

# Keep console.error for production error reporting
./remove_console_logs.sh --keep-errors
```

## Meeting Security

Video meetings use multiple security layers:

- **Server-side tokens** — Agora tokens generated server-side with expiration
- **Access control** — Only the tutor and student for a given session can join
- **Session validation** — Sessions must be in `accepted` or `started` status
- **Middleware protection** — Unauthorized meeting routes are blocked before rendering
- **Periodic checks** — Session status is validated continuously during the call

## Project Structure

```
src/
├── app/              # Next.js App Router pages and API routes
│   ├── dashboard/    # Student and tutor dashboards
│   ├── marketplace/  # Tutor discovery
│   ├── meeting/      # Live video call pages
│   ├── session/      # Session management
│   └── api/          # API route handlers
├── components/       # Shared UI components
├── hooks/            # Custom React hooks
├── lib/              # Utilities and Supabase clients
├── types/            # TypeScript type definitions
└── utils/            # Helper functions
```
