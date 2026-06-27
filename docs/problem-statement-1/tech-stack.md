# Tech Stack: Zo Relationship Mapper

## Build Goal

Localhost proof of concept for:

> Exa-powered LinkedIn/person discovery + OpenAI trust-path ranking for mid-career professionals.

The demo should prove that a user can paste their profile, enter a target role/company, discover relevant public people/company pages through Exa, and receive ranked relationship paths plus outreach drafts.

## Constraints

Use:

- OpenAI API
- Exa API
- Local seed data
- Local browser/server persistence

Do not use:

- Next.js
- Stripe
- Gmail/Google Contacts
- Microsoft Graph
- LinkedIn API
- Direct LinkedIn scraping
- Automated outreach
- Production auth

## Recommended Project Root

If building as a separate app:

```text
zo-relationship-mapper/
```

## Frontend

- Vite
- React
- TypeScript
- TanStack Router if multiple screens are needed
- TanStack Query for calls to local API routes
- Tailwind CSS for fast styling
- shadcn/ui or simple local components if already available
- Lucide React for icons
- Driver.js for guided in-app onboarding and demo tours

Core screens:

- Profile input
- Target opportunity input
- Discovery results
- Ranked trust paths
- Outreach draft
- Outcome tracker

## Demo Tooling

Use two demo layers:

- HyperFrames: external product demo video for hackathon pitch, landing page, README, and async review.
- Driver.js: in-app guided onboarding that moves the user through the real workflow.

The same seeded scenario should power both:

- Persona: mid-career AI/software professional.
- Target: AI product/platform role at a climate tech or sustainability startup in Singapore.
- Outcome: ranked trust path, suggested ask, warm outreach draft, and contacted outcome.

Driver.js tour anchors should map to stable UI elements:

- profile input
- target input
- discover button
- discovered people section
- trust-path ranking section
- outreach draft panel
- outcome tracker

## Local Backend

Use a small Node server so API keys do not live in the browser.

Recommended:

- Node.js
- Hono or Express
- `openai` official SDK
- Exa SDK or direct REST calls
- `dotenv` for local environment variables

Suggested local API endpoints:

```text
POST /api/profile/parse
POST /api/targets/discover
POST /api/trust-paths/rank
POST /api/outreach/draft
GET  /api/demo/seed
```

Endpoint responsibilities:

- `/api/profile/parse`: use OpenAI to extract career history, companies, roles, skills, projects, domains, and proof-of-work from pasted resume/profile text.
- `/api/targets/discover`: use Exa to find public LinkedIn/person/company pages for the target company, role, hiring manager, recruiter, founder, or team.
- `/api/trust-paths/rank`: use OpenAI to rank discovered people against the user's profile and explain the trust path.
- `/api/outreach/draft`: use OpenAI to draft a contextual message.
- `/api/demo/seed`: return fallback demo profile, target, and example Exa-style results.

## Environment Variables

Local `.env`:

```bash
OPENAI_API_KEY=
EXA_API_KEY=
```

Rules:

- Never expose these keys to the browser.
- All OpenAI/Exa calls go through the local backend.

## Data Storage

Hackathon version:

- Local JSON seed files for fallback data.
- Browser `localStorage` for saved targets, ranked paths, and outcome states.

Only add SQLite if the UI needs persistent multi-record workflows.

Suggested local data files:

```text
src/data/demo-profile.json
src/data/demo-targets.json
src/data/demo-people-results.json
```

## Data Model

Minimum entities:

- `UserProfile`
- `CareerItem`
- `TargetOpportunity`
- `DiscoveredPerson`
- `TrustPath`
- `OutreachDraft`
- `Outcome`

Key scoring fields:

- company relevance
- role relevance
- shared background
- hiring proximity
- seniority
- credibility
- outreach friction
- proof-of-work match
- confidence

## AI Responsibilities

OpenAI:

- Parse resume/profile text.
- Normalize career history.
- Explain relationship/trust signals.
- Rank paths.
- Draft outreach.
- Produce structured JSON outputs.

Exa:

- Discover public person/company pages.
- Find people connected to target companies, roles, teams, hiring, recruiting, founders, or communities.
- Retrieve snippets/content that can support relevance scoring.

## Agentic Flow

Keep it simple:

1. Parse user profile.
2. Build Exa query from target.
3. Normalize Exa results.
4. Rank paths.
5. Draft outreach.

No autonomous contacting.

## Testing

Minimum:

- Seed-data happy path works offline except API calls.
- API failures show fallback/demo data.
- Ranked paths render without layout shift.
- Outreach draft can be regenerated.
- Driver.js tour starts, advances, and completes on desktop and narrow mobile.
- HyperFrames storyboard matches the seeded app state and does not depend on live API keys.

Useful tools:

- Vitest for scoring/helper functions.
- Playwright only if there is time for smoke testing.

## Build Order

1. Static UI with seed data.
2. Local backend with `/api/demo/seed`.
3. OpenAI profile parser.
4. Exa target discovery.
5. OpenAI trust-path ranking.
6. Outreach draft.
7. Outcome tracker.
8. Driver.js guided demo tour.
9. HyperFrames storyboard/video export.

## Demo Script

External HyperFrames video:

1. Open with the pain: cold applications are low-trust and noisy.
2. Paste a mid-career professional profile.
3. Enter target: "AI product/platform role at a climate tech startup in Singapore."
4. Run discovery and show public people/company signals.
5. Rank trust paths.
6. Explain why the top path is credible.
7. Generate a warm outreach draft.
8. Mark the path as contacted.

In-app Driver.js tour:

1. Highlight profile input and load the seeded profile.
2. Highlight target input and confirm the target opportunity.
3. Highlight discover and run discovery.
4. Highlight discovered people.
5. Highlight ranked trust paths and select the best path.
6. Highlight outreach draft generation.
7. Highlight outcome tracker.
