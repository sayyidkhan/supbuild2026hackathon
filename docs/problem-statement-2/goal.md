# Goal Brief: Zo Expert

This file is atomic. A fresh agent session should be able to read only this file and implement the project without relying on prior chat history. Supporting docs are useful but optional.

Supporting docs, if more context is needed:

- `docs/problem-statement-2/problem-statement.md`
- `docs/problem-statement-2/prd.md`
- `docs/problem-statement-2/research.md`
- `docs/problem-statement-2/tech-stack.md`

## Copy-Paste `/goal`

```text
/goal Build the Zo Expert localhost proof of concept in ./zo-expert.

Product: AI consultation proxy for SME owners. A small business owner defines business knowledge, tone, policies, and escalation rules. A non-technical customer, prospect, or staff member asks questions through a simple consultation interface. OpenAI answers in the owner's style when safe, escalates risky questions, and produces an owner brief. Exa is optional and only used for public enrichment when useful.

Target buyer: small SME owner-operators doing roughly $0-$1M annual revenue, strongest beachhead S$100k-S$750k annual revenue, 1-8 staff, owner-led operations.

End user: non-technical customers, prospects, or staff who want to consult the owner, clarify services, ask business questions, or get next-step guidance.

JTBD: When non-technical customers or staff need the business owner's expertise but the owner is busy, help them consult an AI owner proxy that understands the business, answers in the owner's style, and escalates only questions that need human judgment.

Hard constraints:
- Use Vite + React + TypeScript.
- Use TanStack Router only if routing is needed.
- Use TanStack Query for local API calls.
- Use a local Node backend with Hono or Express.
- Use OpenAI API and optional Exa API only.
- Keep API keys server-side.
- Must run on localhost.
- Must work with seed/demo data even when API keys are missing.
- Do not use Next.js.
- Do not use Stripe.
- Do not use WhatsApp, Gmail, Microsoft Graph, QuickBooks, Xero, accounting, or CRM integrations.
- Do not build full autonomous sending.

Use two implementation agents:
1. Frontend/Product Agent owns the React UI, owner setup, consultation chat, escalation review, and owner brief.
2. AI/API Agent owns the local backend, OpenAI/Exa service wrappers, consultation answer logic, escalation logic, owner brief generation, and seed fallback responses.

Main orchestrator owns scaffolding, package scripts, dependency installation, shared types/API contract, final integration, testing, and starting the dev server.

Acceptance criteria:
- `npm install` works inside ./zo-expert.
- One command starts the app locally.
- Owner can define or load business knowledge, FAQs, policies, tone, and escalation rules.
- Non-technical user can ask consultation questions.
- App answers safe questions in owner style.
- App escalates sensitive or high-risk questions instead of answering blindly.
- App shows owner brief: answered questions, escalations, knowledge gaps, and suggested updates.
- App works with seed data without API keys.
- App has a clean, demoable UI and does not expose API keys.
```

## Product Context

Zo Expert is not a generic chatbot, CRM, WhatsApp bot, payment tool, or enterprise workflow automation product.

It exists for one narrow moment:

> A non-technical customer, prospect, or staff member needs the business owner's judgment, but the owner is busy.

The demo should emphasize owner-style consultation:

- owner business knowledge
- owner tone and policies
- consultation chat for non-technical users
- safe answer vs escalation
- knowledge gaps
- owner brief

## User And Buyer

Buyer:

- Small SME owner-operator.
- $0-$1M annual revenue.
- Strongest wedge: S$100k-S$750k revenue, 1-8 staff.
- Owner still answers repeated questions and makes routine decisions.

End users:

- Customers.
- Prospects.
- Staff.
- Event/community attendees.

Best-fit businesses:

- Appointment-led services.
- Quote-led services.
- Expertise-led service businesses.
- Home services.
- Renovation/repair.
- Beauty/wellness.
- Tuition/enrichment.
- Clinics.
- Small agencies.

Pain:

- Owner keeps answering repeated questions.
- Staff cannot make decisions without owner.
- Prospects need guidance before buying/booking.
- Owner cannot scale access to their judgment.

Willingness-to-pay moment:

- Repeated questions consume owner time.
- Slow replies reduce conversion.
- Staff repeatedly interrupt owner.
- Owner wants to preserve standards while increasing access.

## What To Build

Build one app in:

```text
./zo-expert
```

Expected user flow:

1. Owner loads or defines business profile.
2. Owner defines services, FAQs, policies, tone, and escalation rules.
3. Non-technical user asks a question.
4. App answers in owner style if safe.
5. App escalates if the question is risky, sensitive, missing context, or outside policy.
6. App logs consultation outcome.
7. App produces owner brief:
   - answered questions
   - escalations
   - knowledge gaps
   - suggested updates

## What Not To Build

Do not build:

- Generic chatbot.
- WhatsApp integration.
- Gmail integration.
- CRM.
- Accounting or payment tool.
- Stripe/subscription flow.
- Full autonomous sending.
- Enterprise workflow automation.

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
- Exa SDK or direct Exa REST calls, optional
- `dotenv`

Persistence:

- Local JSON seed data.
- Browser `localStorage` for owner settings, consultation history, and brief state.
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

- `zo-expert/src/App.tsx`
- `zo-expert/src/routes/*`
- `zo-expert/src/components/*`
- `zo-expert/src/data/*`
- `zo-expert/src/styles.css`
- UI-facing TypeScript types if they do not conflict with shared API types.

Responsibilities:

- Build the demo UI.
- Keep the flow simple:
  1. Owner setup
  2. Knowledge base
  3. Consultation chat
  4. Escalation review
  5. Owner brief
  6. Knowledge gaps
- Make the app usable with seed data.
- Show clear safe-answer vs escalation states.
- Make it obvious this is not a generic chatbot.

Frontend acceptance criteria:

- Non-technical user can ask a question without learning a tool.
- Owner-style answers show which business rule/FAQ was used.
- Escalations show reason and suggested owner action.
- Owner brief is scannable and useful.
- UI works on desktop and a narrow mobile viewport.

### Agent 2: AI/API Agent

Ownership:

- `zo-expert/server/*`
- `zo-expert/src/lib/api.ts`
- `zo-expert/src/types/api.ts`
- `zo-expert/.env.example`
- Seed response helpers used by API endpoints.

Responsibilities:

- Build local backend with Hono or Express.
- Keep OpenAI and Exa keys server-side.
- Implement API endpoints.
- Provide seed fallback responses when keys are missing or APIs fail.
- Return structured JSON responses for frontend consumption.
- Implement lightweight agentic loop:
  1. Retrieve relevant business knowledge.
  2. Draft owner-style answer.
  3. Check escalation rules.
  4. Return answer or escalation.
  5. Detect knowledge gaps.

Backend acceptance criteria:

- API starts locally.
- Missing API keys do not break the demo.
- Safe questions return owner-style answers.
- Risky questions return escalation objects.
- Owner brief summarizes answered, escalated, and unresolved questions.

## API Contract

Suggested endpoints:

```text
GET  /api/demo/seed
POST /api/owner-profile/build
POST /api/consult
POST /api/escalation/check
POST /api/brief/generate
POST /api/enrich
```

### `POST /api/owner-profile/build`

Input:

```json
{
  "businessName": "...",
  "services": ["..."],
  "faqs": [],
  "policies": [],
  "tone": "warm, practical, concise",
  "escalationRules": []
}
```

Output:

```json
{
  "ownerProfile": {
    "businessSummary": "...",
    "voiceRules": ["..."],
    "serviceRules": ["..."],
    "escalationRules": ["..."]
  }
}
```

### `POST /api/consult`

Input:

```json
{
  "question": "...",
  "ownerProfile": {},
  "knowledgeBase": {}
}
```

Output:

```json
{
  "status": "answered",
  "answer": "...",
  "usedKnowledge": ["..."],
  "confidence": "high",
  "needsEscalation": false,
  "knowledgeGaps": []
}
```

Escalation output:

```json
{
  "status": "escalated",
  "answer": null,
  "reason": "...",
  "suggestedOwnerAction": "...",
  "safeDraft": "...",
  "knowledgeGaps": ["..."]
}
```

### `POST /api/brief/generate`

Input:

```json
{
  "consultations": []
}
```

Output:

```json
{
  "summary": "...",
  "answeredCount": 4,
  "escalatedCount": 2,
  "knowledgeGaps": ["..."],
  "suggestedUpdates": ["..."]
}
```

## Shared Demo Data

Use seed data for:

- Appointment-led service business.
- Owner tone and policies.
- FAQs and service descriptions.
- Safe customer questions.
- Staff exception questions.
- Risky questions that must escalate.
- Owner brief examples.

Seed business should be concrete enough for a judge to understand:

- business name
- target customer
- services
- pricing guidelines
- common FAQs
- policies
- escalation rules
- owner tone

## Demo Script

1. Show owner setup and knowledge base.
2. Ask: "Which service should I choose for my situation?"
3. Show owner-style answer.
4. Ask: "Can you waive this policy / handle this exception?"
5. Show escalation instead of unsafe answer.
6. Show owner brief with answered questions, escalations, and knowledge gaps.

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
2. Scaffold `./zo-expert`.
3. Spawn the two implementation agents exactly by ownership boundary.
4. Keep API/backend work separate from UI work.
5. Integrate only after both agents finish their owned slices.
6. Run the app locally and verify the fallback path before using real API keys.
