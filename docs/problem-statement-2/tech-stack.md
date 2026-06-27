# Tech Stack: Zo Expert

## Build Goal

Localhost proof of concept for:

> A non-technical consultation interface where customers, prospects, or staff can consult an SME owner's business knowledge through an AI owner proxy.

The demo should prove that an SME owner can define their business knowledge and escalation rules, then a non-technical user can ask questions and receive owner-style answers or escalation.

## Constraints

Use:

- OpenAI API
- Exa API only when external/public context is useful
- Local seed data
- Local browser/server persistence
- Optional lightweight agentic loop

Do not use:

- Next.js
- Stripe
- WhatsApp integration
- Gmail or Microsoft Graph
- QuickBooks/Xero/accounting integrations
- Full CRM integrations
- Production auth

## Recommended Project Root

If building as a separate app:

```text
zo-expert/
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

Core screens:

- Owner setup
- Knowledge base editor
- Consultation chat
- Escalation review
- Owner brief
- Knowledge gaps

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
POST /api/owner-profile/build
POST /api/consult
POST /api/escalation/check
POST /api/brief/generate
POST /api/enrich
GET  /api/demo/seed
```

Endpoint responsibilities:

- `/api/owner-profile/build`: use OpenAI to normalize owner profile, services, FAQs, policies, tone, and escalation rules.
- `/api/consult`: answer a user question using local business knowledge and owner style.
- `/api/escalation/check`: decide whether a question should be answered, drafted for owner approval, or escalated.
- `/api/brief/generate`: summarize consultations, escalations, unanswered questions, and suggested knowledge-base updates.
- `/api/enrich`: optional Exa enrichment for public context, examples, market references, or business-specific external facts.
- `/api/demo/seed`: return fallback business profile, knowledge base, and sample consultation prompts.

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

- Local JSON seed files for fallback business data.
- Browser `localStorage` for owner settings, consultation history, escalation state, and knowledge gaps.

Only add SQLite if the owner brief needs more durable multi-session history.

Suggested local data files:

```text
src/data/demo-business.json
src/data/demo-faqs.json
src/data/demo-policies.json
src/data/demo-consultations.json
```

## Data Model

Minimum entities:

- `OwnerProfile`
- `BusinessProfile`
- `Service`
- `Policy`
- `FAQ`
- `Consultation`
- `Answer`
- `Escalation`
- `KnowledgeGap`
- `OwnerBrief`

Escalation fields:

- risk level
- reason
- suggested owner action
- safe draft answer
- missing knowledge

## AI Responsibilities

OpenAI:

- Normalize owner/business knowledge.
- Answer in owner style.
- Detect risky or sensitive questions.
- Decide answer vs escalate.
- Identify missing knowledge.
- Generate owner brief.

Exa:

- Optional enrichment only.
- Pull public context when a question needs external examples, market context, or public business references.
- Do not make Exa required for the core demo.

## Agentic Flow

Optional lightweight loop:

1. Receive question.
2. Retrieve relevant local business knowledge.
3. Draft answer.
4. Check escalation rules.
5. If safe, return answer.
6. If not safe, return escalation with owner-facing summary.
7. Log knowledge gap if the answer required missing business context.

No autonomous sending or real-world execution.

## Testing

Minimum:

- Seed business profile loads.
- Consultation chat answers common questions.
- Escalation triggers for sensitive questions.
- Owner brief summarizes answered, escalated, and unresolved questions.
- API failures show fallback demo response.

Useful tools:

- Vitest for escalation-rule helpers.
- Playwright only if there is time for smoke testing.

## Build Order

1. Static UI with seed business data.
2. Consultation chat using local mock responses.
3. Local backend with `/api/demo/seed`.
4. OpenAI consultation answer.
5. Escalation check.
6. Owner brief.
7. Optional Exa enrichment.

## Demo Script

1. Show SME owner profile and business rules.
2. Open non-technical consultation chat.
3. Ask a common customer question.
4. Show owner-style answer.
5. Ask a risky exception question.
6. Show escalation instead of unsafe answer.
7. Show owner brief and knowledge gaps.
