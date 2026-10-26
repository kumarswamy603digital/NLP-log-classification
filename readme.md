# FounderRadar

Autonomous startup idea pipeline that continuously monitors real-world pain signals across Reddit, Hacker News, GitHub, Product Hunt, and Stack Overflow, synthesizing them with LLM extractors into daily ranked, high-demand venture opportunities.

---

## Market Need

Most startup founders waste months building products that nobody needs. FounderRadar turns the discovery process inside out: rather than inventing speculative ideas, it scans thousands of real customer complaints, feature requests, and workflow frustrations posted across developer communities to unearth verifiable, monetizable software opportunities.

---

## Architecture & Data Pipeline

```
┌────────────────────────────────────────────────────────┐
│               Cross-Platform Ingestion                 │
│  - Reddit (PullPush.io)    - Hacker News (Algolia API) │
│  - GitHub Issues & PRs     - Product Hunt (GraphQL)    │
│  - Stack Overflow API      - Rate Limit Coalescers     │
└───────────────────────────┬────────────────────────────┘
                            │ Raw Pain Signals
                            ▼
┌────────────────────────────────────────────────────────┐
│             LLM Extraction & Ranking Engine            │
│  - Demand Intensity Scoring (0-100)                    │
│  - Willingness-to-Pay & Target Buyer Inference         │
│  - Technical Feasibility & Solution Architecture       │
└───────────────────────────┬────────────────────────────┘
                            │ Ranked Opportunities
                            ▼
┌────────────────────────────────────────────────────────┐
│               FounderRadar Web Client                  │
│       (Next.js 14 App Router + React + Tailwind)       │
└────────────────────────────────────────────────────────┘
```

---

## Key Capabilities

- **Omnichannel Signal Ingestion**: Automated collectors scan Reddit founder subreddits, Hacker News 'Ask HN' threads, GitHub issues, Product Hunt launches, and Stack Overflow discussions.
- **Strict Deduplication & Windowing**: Global deduplication by stable platform IDs, rolling 24-hour UTC window boundaries, and exponential backoff retry policies.
- **Automated Opportunity Ranking**: Computes composite demand scores, addressable audience definitions, and estimated MRR potential for each emerging pain point.
- **Dynamic Live Radar UI**: Fast Next.js 14 App Router interface featuring instant keyword filtering, platform breakdowns, and pain-to-solution side-by-side matrices.
- **Serverless Cron Handlers**: Ready for automated edge triggers via Vercel Cron or GitHub Actions (`/api/cron/collect` and `/api/cron/process`).

---

## Technology Stack

- **Framework**: Next.js 14 (App Router, React 18, TypeScript)
- **Styling**: Tailwind CSS, PostCSS, Autoprefixer
- **Data Persistence**: Supabase (PostgreSQL, Row Level Security)
- **Data Fetchers**: Native HTTP with AbortController timeouts and custom rate limiters

---

## Quickstart

### Prerequisites

- Node.js 18.17+ or higher
- npm or bun

### Installation

```bash
git clone https://github.com/kumarswamy603digital/searches-.git
cd searches-
npm install
```

### Environment Setup

Create `.env.local` based on `.env.local.example`:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
CRON_SECRET=your_random_secret_token
GITHUB_TOKEN=your_github_personal_access_token
PRODUCTHUNT_TOKEN=your_producthunt_developer_token
```

### Local Development

```bash
npm run dev
```

### Production Build

```bash
npm run build
npm start
```

---

## Cloud Deployment

Deploy seamlessly to Vercel:

```bash
vercel --prod
```

Configure `CRON_SECRET` in project settings to secure the automated ingestion cron endpoints.

