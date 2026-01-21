# OccupAI

**Real-time occupancy intelligence for physical spaces.**

OccupAI is a modern SaaS platform that enables venues to monitor and analyze foot traffic across their locations using edge-deployed cameras and AI-powered detection.

## What We Do

We help multi-location businesses understand how their physical spaces are being used in real-time:

- **Hotels & Hospitality** — Monitor lobby traffic, pool areas, restaurants, and conference rooms
- **Restaurants & Bars** — Track dining room capacity, bar occupancy, and patio usage
- **Fitness Centers** — See real-time gym floor, studio, and locker room occupancy
- **Retail Stores** — Analyze foot traffic patterns across departments and checkout areas

## How It Works

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Cameras   │ ──▶ │ Edge Device │ ──▶ │  OccupAI    │ ──▶ │  Dashboard  │
│  (On-site)  │     │ (Tailscale) │     │   Cloud     │     │  Analytics  │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

1. **Cameras** capture video at your location
2. **Edge devices** process feeds locally using AI (privacy-first — video never leaves your premises)
3. **Occupancy data** is securely transmitted to OccupAI via encrypted Tailscale network
4. **Dashboards** provide real-time metrics and historical trend analysis

## Key Features

| Feature | Description |
|---------|-------------|
| **Real-Time Tracking** | See live occupancy counts across all your locations |
| **Area-Level Granularity** | Track 30+ area types: dining, lobby, gym, checkout, VIP sections, and more |
| **Multi-Location Support** | Manage unlimited locations under one organization |
| **Privacy-First** | Edge processing means video stays on-premise |
| **Role-Based Access** | Organization admins, members, and internal admin tiers |
| **Trend Analytics** | 7-day, 30-day, and 90-day occupancy trend visualization |
| **Secure Networking** | Tailscale-powered zero-trust device connectivity |

## Tech Stack

**Frontend**
- Next.js 16 (App Router)
- React 19
- TypeScript
- Tailwind CSS + Radix UI
- Recharts

**Backend**
- Next.js Server Actions
- PostgreSQL + Prisma ORM
- Clerk Authentication
- Tailscale API Integration

**Infrastructure**
- Digital Ocean + Docker Swarm for deployment
- Tailscale for edge device networking
- LocationIQ for geocoding
- Resend for transactional email
- Cloudinary for media storage

## Area Types Supported

OccupAI supports tracking across a wide variety of venue areas:

| Category | Areas |
|----------|-------|
| **Food & Beverage** | Bar, Dining, Kitchen, Outdoor Patio |
| **Entry & Transit** | Entrance, Exit, Lobby, Hallway, Stairwell, Elevator |
| **Guest Services** | Waiting, Reception, Restroom, Checkout |
| **Entertainment** | Stage, Dance Floor, Gaming Area, Pool Area |
| **Fitness** | Gym, Spa |
| **Retail** | Retail Floor, Showroom |
| **Private Spaces** | VIP Section, Private Room, Conference Room, Office |
| **Outdoor** | Parking, Courtyard, Rooftop |
| **Utility** | Storage, Loading Dock |

## Getting Started

```bash
# Clone the repository
git clone https://github.com/Occupai-25/occupai.git

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env

# Run database migrations
npx prisma migrate dev

# Start development server
npm run dev
```

## Environment Variables

```env
# =============================================================================
# Database
# =============================================================================
DATABASE_URL=postgresql://user:password@host:5432/database

# =============================================================================
# Authentication (Clerk)
# =============================================================================
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...
CLERK_WEBHOOK_SIGNING_SECRET=whsec_...

# Clerk URLs
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_SIGN_IN_FORCE_REDIRECT_URL=/dashboard
NEXT_PUBLIC_CLERK_SIGN_UP_FORCE_REDIRECT_URL=/dashboard

# =============================================================================
# Tailscale
# =============================================================================
# Generate API key at: https://login.tailscale.com/admin/settings/keys
TAILSCALE_API_KEY=tskey-api-...
TAILSCALE_API_URL=https://api.tailscale.com/api/v2
TAILSCALE_API_TAILNET=your-tailnet.com
TAILSCALE_AUTH_KEY=tskey-auth-...
TAILSCALE_HOSTNAME=your-app.tailnet.ts.net

# =============================================================================
# Email (Resend)
# =============================================================================
RESEND_API_KEY=re_...
ADMIN_EMAILS=admin@yourdomain.com

# =============================================================================
# Media Storage (Cloudinary)
# =============================================================================
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=your-cloud-name
NEXT_PUBLIC_CLOUDINARY_API_KEY=your-api-key
CLOUDINARY_API_SECRET=your-api-secret

# =============================================================================
# Geocoding (LocationIQ)
# =============================================================================
LOCATIONIQ_API_KEY=pk....
```

## Deployment

OccupAI is deployed on **Digital Ocean** using **Docker Swarm** for container orchestration.

```bash
# Build the Docker image
docker build -t occupai:latest .

# Deploy to Docker Swarm
docker stack deploy -c docker-compose.yml occupai
```

### Infrastructure Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Digital Ocean                           │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                  Docker Swarm                        │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │   │
│  │  │  OccupAI    │  │  OccupAI    │  │  PostgreSQL │  │   │
│  │  │  (Primary)  │  │  (Replica)  │  │     DB      │  │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │   │
│  └─────────────────────────────────────────────────────┘   │
│                           │                                 │
│                     Tailscale VPN                          │
│                           │                                 │
└───────────────────────────┼─────────────────────────────────┘
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
      ┌──────────┐   ┌──────────┐   ┌──────────┐
      │  Edge    │   │  Edge    │   │  Edge    │
      │ Device 1 │   │ Device 2 │   │ Device N │
      └──────────┘   └──────────┘   └──────────┘
```

## License

Proprietary — All rights reserved.

---

<p align="center">
  <strong>OccupAI</strong> — Know your space. In real-time.
</p>
