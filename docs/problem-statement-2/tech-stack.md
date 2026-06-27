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
- Driver.js for guided in-app onboarding and demo tours

Core screens:

- Owner setup
- Knowledge base editor
- Consultation chat
- Escalation review
- Owner brief
- Knowledge gaps

## Demo Tooling

Use two demo layers:

- HyperFrames: external product demo video for hackathon pitch, landing page, README, and async review.
- Driver.js: in-app guided onboarding that moves the user through the real workflow.

The same seeded scenario should power both:

- Persona: SME owner-operator.
- Business: appointment-led service business.
- End user: non-technical customer, prospect, or staff member.
- Outcome: owner-style answer, escalation for risky exception, owner brief, and knowledge gaps.

Driver.js tour anchors should map to stable UI elements:

- admin workspace
- sample or blank template action
- services/FAQs/policies editor
- escalation rules editor
- user portal switch
- consultation composer
- conversation outcome card
- owner brief panel

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
- Driver.js tour starts, advances, and completes on desktop and narrow mobile.
- HyperFrames storyboard matches the seeded app state and does not depend on live API keys.

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
8. Driver.js guided demo tour.
9. HyperFrames storyboard/video export.

## Demo Script

External HyperFrames video:

1. Open with the pain: the owner is the business bottleneck.
2. Load the SME owner template.
3. Show services, FAQs, policies, tone, and escalation rules.
4. Ask a common customer question.
5. Show the owner-style answer.
6. Ask a risky exception question.
7. Show escalation instead of unsafe answer.
8. Show owner brief and knowledge gaps.

In-app Driver.js tour:

1. Highlight Admin Workspace and load the sample template.
2. Highlight business rules and knowledge base sections.
3. Highlight escalation boundaries.
4. Switch to User Portal.
5. Highlight the consultation composer and ask a common question.
6. Highlight the escalation outcome for a risky question.
7. Highlight owner brief and knowledge gaps.
