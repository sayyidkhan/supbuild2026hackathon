# Goal Brief: Zo Relationship Mapper

This file is atomic. A fresh agent session should be able to read only this file and implement the project without relying on prior chat history. Supporting docs are useful but optional.

Supporting docs, if more context is needed:

- `docs/problem-statement-1/problem-statement.md`
- `docs/problem-statement-1/prd.md`
- `docs/problem-statement-1/research.md`
- `docs/problem-statement-1/tech-stack.md`

## Copy-Paste `/goal`

```text
/goal Build the Zo Relationship Mapper localhost proof of concept in ./zo-relationship-mapper.

Product: Exa-powered relationship trust-path mapper for mid-career professionals. A user pastes their resume/profile, enters a target role/company/person, Exa discovers relevant public LinkedIn/person/company pages, OpenAI ranks the best trust paths, and the app drafts a contextual outreach message.

Target user: mid-career and senior working professionals with 5-20 years of experience, strongest beachhead 30-42 years old with 7-15 years of experience. They have enough resume depth, career history, network density, and willingness to pay for career leverage.

JTBD: When I find a high-value career opportunity but do not have obvious access, help me map the fastest credible trust path through my real career history and relationships, so I can make a warm, contextual move instead of relying on cold applications.

Hard constraints:
- Use Vite + React + TypeScript.
- Use TanStack Router only if routing is needed.
- Use TanStack Query for local API calls.
- Use a local Node backend with Hono or Express.
- Use OpenAI API and Exa API only.
- Keep API keys server-side.
- Must run on localhost.
- Must work with seed/demo data even when API keys are missing.
- Do not use Next.js.
- Do not use Stripe.
- Do not use Gmail, Google Contacts, Microsoft Graph, LinkedIn API, direct LinkedIn scraping, or automated outreach.

Use two implementation agents:
1. Frontend/Product Agent owns the React UI, demo flow, local state, and visual polish.
2. AI/API Agent owns the local backend, OpenAI/Exa service wrappers, seed fallback responses, and API contracts.

Main orchestrator owns scaffolding, package scripts, dependency installation, shared types/API contract, final integration, testing, and starting the dev server.

Acceptance criteria:
- `npm install` works inside ./zo-relationship-mapper.
- One command starts the app locally.
- User can paste a resume/profile and enter a target.
- App can run Exa discovery or fallback to seed Exa-style results.
- App displays discovered people/company pages.
- App ranks trust paths with explanations.
- App generates a contextual outreach draft.
- App tracks simple outcome states: not contacted, contacted, replied, referral, dead end.
- App has a clean, demoable UI and does not expose API keys.
```

## Product Context

Zo Relationship Mapper is not a career coach, resume tool, job board, or CRM.

It exists for one narrow moment:

> A working professional has a target opportunity and wants to know who is the most credible person to contact before applying cold.

The demo should emphasize trust-path discovery:

- target role/company/person
- public people/company discovery through Exa
- profile-to-person relevance reasoning through OpenAI
- ranked paths with explanations
- warm outreach draft
- simple outcome tracking

## User And Buyer

Primary user:

- Mid-career/senior professional.
- 5-20 years of experience.
- Strongest wedge: 7-15 years experience, age 30-42.
- Likely functions: software, AI, product, consulting, finance, sustainability, operations, strategy, GTM.

Pain:

- Cold applications feel like a black hole.
- Existing network is underused.
- They do not know which weak tie or public person creates the best trust path.
- They want higher odds of referral, advice call, intro, or interview.

Willingness-to-pay moment:

- Active job/opportunity search.
- Switching company, role, industry, or function.
- Targeting senior/high-compensation roles.
- Trying to avoid cold application noise.

## What To Build

Build one app in:

```text
./zo-relationship-mapper
```

Expected user flow:

1. User pastes resume/profile.
2. User enters target role/company/person.
3. App parses profile into companies, roles, skills, domains, proof-of-work.
4. App queries Exa for public LinkedIn/person/company pages related to the target.
5. App shows discovered people.
6. App ranks best trust paths.
7. App explains why each path is credible.
8. App drafts outreach.
9. User marks outcome state.

## What Not To Build

Do not build:

- Full CRM.
- Job board.
- Career advice chatbot.
- Resume optimizer.
- LinkedIn scraper.
- Gmail/contacts importer.
- Stripe or subscription flow.
- Automated outreach sender.

## Tech Stack

Frontend:

- Vite
- React
- TypeScript
- TanStack Query
- TanStack Router only if route structure is useful
- Tailwind CSS or simple CSS
- Lucide React for icons if needed

Backend:

- Local Node server
- Hono or Express
- `openai` official SDK
- Exa SDK or direct Exa REST calls
- `dotenv`

Persistence:

- Local JSON seed data.
- Browser `localStorage` for target history, ranked paths, and outcomes.
- Avoid database unless absolutely necessary.

Environment:

```bash
OPENAI_API_KEY=
EXA_API_KEY=
```

Key rule:

> API keys must stay server-side. The browser calls only local backend endpoints.

## Agent Split

### Agent 1: Frontend/Product Agent

Ownership:

- `zo-relationship-mapper/src/App.tsx`
- `zo-relationship-mapper/src/routes/*`
- `zo-relationship-mapper/src/components/*`
- `zo-relationship-mapper/src/data/*`
- `zo-relationship-mapper/src/styles.css`
- UI-facing TypeScript types if they do not conflict with shared API types.

Responsibilities:

- Build the end-to-end demo UI.
- Keep the flow simple and linear:
  1. Profile input
  2. Target input
  3. Discovery results
  4. Ranked trust paths
  5. Outreach draft
  6. Outcome tracker
- Make the app usable without real API calls through seed data.
- Show loading, error, and fallback states.
- Make it obvious this is not a generic CRM or career coach.

Frontend acceptance criteria:

- User can complete the demo flow in under 2 minutes.
- Ranked path cards show person, role, company, trust reason, confidence, and suggested ask.
- Outreach draft can be regenerated.
- Outcome state can be updated locally.
- UI works on desktop and a narrow mobile viewport.

### Agent 2: AI/API Agent

Ownership:

- `zo-relationship-mapper/server/*`
- `zo-relationship-mapper/src/lib/api.ts`
- `zo-relationship-mapper/src/types/api.ts`
- `zo-relationship-mapper/.env.example`
- Seed response helpers used by API endpoints.

Responsibilities:

- Build local backend with Hono or Express.
- Keep OpenAI and Exa keys server-side.
- Implement API endpoints.
- Provide seed fallback responses when keys are missing or APIs fail.
- Return structured JSON responses for frontend consumption.

Backend acceptance criteria:

- API starts locally.
- Missing API keys do not break the demo.
- API returns typed JSON for all core endpoints.
- OpenAI prompts request structured JSON output.
- Exa query construction is target-aware.

## API Contract

Suggested endpoints:

```text
GET  /api/demo/seed
POST /api/profile/parse
POST /api/targets/discover
POST /api/trust-paths/rank
POST /api/outreach/draft
```

### `POST /api/profile/parse`

Input:

```json
{
  "profileText": "..."
}
```

Output:

```json
{
  "careerSummary": "...",
  "companies": ["..."],
  "roles": ["..."],
  "skills": ["..."],
  "domains": ["..."],
  "proofOfWork": ["..."]
}
```

### `POST /api/targets/discover`

Input:

```json
{
  "target": "AI product role at ExampleCo",
  "parsedProfile": {}
}
```

Output:

```json
{
  "results": [
    {
      "name": "...",
      "title": "...",
      "company": "...",
      "url": "https://...",
      "source": "exa",
      "snippet": "...",
      "signals": ["hiring proximity", "shared domain"]
    }
  ]
}
```

### `POST /api/trust-paths/rank`

Input:

```json
{
  "target": "...",
  "parsedProfile": {},
  "discoveredPeople": []
}
```

Output:

```json
{
  "paths": [
    {
      "personName": "...",
      "role": "...",
      "company": "...",
      "score": 86,
      "confidence": "high",
      "trustReason": "...",
      "suggestedAsk": "...",
      "risks": ["..."]
    }
  ]
}
```

### `POST /api/outreach/draft`

Input:

```json
{
  "target": "...",
  "selectedPath": {},
  "tone": "warm, concise, non-desperate"
}
```

Output:

```json
{
  "subject": "...",
  "message": "...",
  "followUp": "..."
}
```

## Shared Demo Data

Use seed data for:

- Mid-career AI/software professional profile.
- Target company and role.
- Exa-style people results.
- Ranked trust-path examples.
- Outreach drafts.

Seed profile should include enough career detail to make ranking legible:

- prior companies
- AI/software skills
- consulting or banking background if useful
- hackathon/community signals
- sustainability or agentic AI domain interest

## Demo Script

1. Paste a profile.
2. Enter target: "AI product/platform role at a climate tech startup."
3. Click discover.
4. Show Exa-style public people/company results.
5. Click rank trust paths.
6. Explain top path.
7. Generate outreach draft.
8. Mark outcome as contacted.

## Final Verification

Before final response:

- Run install if dependencies are new.
- Run lint/typecheck if configured.
- Start local dev server.
- Open app in browser if browser tooling is available.
- Confirm fallback demo path works without API keys.
- Report local URL and any env vars needed.

## Fresh Session Instructions

If starting from a brand-new session:

1. Read this file completely.
2. Scaffold `./zo-relationship-mapper`.
3. Spawn the two implementation agents exactly by ownership boundary.
4. Keep API/backend work separate from UI work.
5. Integrate only after both agents finish their owned slices.
6. Run the app locally and verify the fallback path before using real API keys.
