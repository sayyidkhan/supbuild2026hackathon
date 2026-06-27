# PRD: AI Digital Twin for SME Owners

## 1. Product Summary

Working name: Zo Expert

One-liner:

> Let non-technical customers, prospects, or staff consult an SME owner's business expertise through an AI owner proxy that answers in the owner's style and escalates what needs human judgment.

## 2. Target User

Primary user:

- Buyer: small SME owner-operators.
- End user: non-technical customers, prospects, or staff who want to consult the business owner, ask questions, clarify services, or get next-step guidance.
- Small SME owner-operators.
- Roughly $0-$1M annual revenue.
- Strongest beachhead: S$100k-S$750k annual revenue.
- 1-8 staff.
- Owner still answers repeated questions, explains services, qualifies requests, gives recommendations, and decides what needs escalation.

## 3. JTBD

When non-technical customers or staff need the business owner's expertise but the owner is busy, help them consult an AI owner proxy that understands the business, answers in the owner's style, and escalates only the questions that need human judgment.

## 4. Problem

Small business owners are the router, memory, and decision engine of the business. Customers, prospects, and staff often need the owner's judgment, but the owner cannot personally answer every repeated consultation, service question, and next-step request.

## 5. MVP Scope

Build a localhost demo for **Zo Expert**, an AI consultation proxy for SME owners.

Implementation goal brief: [goal.md](./goal.md)

Core flow:

1. Owner enters business profile and operating rules.
2. Owner enters services, policies, FAQs, preferences, and escalation rules.
3. Non-technical end user asks a business question in a simple chat/consultation interface.
4. App uses OpenAI to answer in the owner's style from the business knowledge base.
5. App uses Exa when useful to enrich public context, examples, or market references.
6. App flags questions that should be escalated to the real owner.
7. App shows the owner a brief of consultations, escalations, and unanswered knowledge gaps.

## 6. Core Features

- Owner/business profile
- Business rules and tone settings
- Non-technical consultation chat
- Business knowledge base
- Owner-style answer generator
- Escalation rule detection
- Consultation summary for the owner
- Knowledge gap detection
- Optional Exa enrichment for public/business context
- Approve/edit/ignore states

## 7. Non-Goals

- Real WhatsApp integration
- Real payment collection
- Full CRM
- Full accounting integration
- Multi-user permissions
- Fully autonomous sending
- Enterprise workflow automation
- Stripe or payment integration
- Gmail, Microsoft Graph, QuickBooks, Xero, or other third-party workflow integrations

## 8. User Stories

- As a non-technical customer, I want to ask questions in plain language and get an answer that reflects how the owner would guide me.
- As a staff member, I want to ask operational questions without interrupting the owner every time.
- As an SME owner, I want the AI to answer repeated questions using my business rules and tone.
- As an SME owner, I want sensitive or high-risk questions escalated instead of answered automatically.
- As an SME owner, I want to see what customers and staff asked while I was busy.

## 9. Demo Data

Seed sample:

- Business type: appointment-led service business.
- Example verticals: renovation, beauty/wellness, tuition, clinic, home service, agency.
- Business knowledge:
  - services
  - pricing guidelines
  - FAQs
  - owner preferences
  - policies
  - escalation rules
- Consultation prompts:
  - customer asking which service fits their situation
  - customer asking for price range and next steps
  - staff asking whether to accept an exception
  - customer asking a question that should be escalated
  - customer asking for preparation instructions before an appointment

## 10. Success Metrics

Hackathon demo success:

- Can explain the target SME owner in under 20 seconds.
- Can show a non-technical user consulting the owner's AI proxy.
- Can show owner-style, business-specific answers.
- Can show escalation for questions that need the actual owner.
- Can show an owner brief with consultation history and knowledge gaps.
- Can show why this is not a generic chatbot: it uses owner rules, business memory, and escalation boundaries.

Product validation metrics:

- Owner says the consultation proxy would reduce repeated interruptions.
- Owner would trust it to handle repeated customer/staff questions with approval boundaries.
- Non-technical users can get useful answers without learning a tool.
- Owner identifies at least one repeated customer/staff question that Zo Expert can handle safely.

## 11. Open Questions

- Which vertical should be the first demo: home services, beauty/wellness, tuition, clinic, or agency?
- Should the first end user be customers, staff, or prospects?
- What questions should always be escalated to the owner?
- Should the product be sold as a public consultation portal, internal staff expert, or both?

## 12. API Constraints

Use only:

- OpenAI API
- Exa API when external/public context is useful
- Local seed data / browser storage

Optional:

- Lightweight agentic loop inside the app: answer, check escalation rules, detect knowledge gaps, produce owner brief.

Do not use:

- Stripe
- WhatsApp integration
- Gmail or Microsoft Graph
- QuickBooks/Xero/accounting integrations
- Full CRM integrations

## 13. Localhost Tech Stack

Detailed stack: [tech-stack.md](./tech-stack.md)

Localhost-only fast path:

- Vite + React
- TanStack Router if routing is needed
- TanStack Query for API calls/state around OpenAI/Exa requests
- Local JSON seed data for business profile, FAQs, policies, and sample consultation prompts
- Browser localStorage for consultation history and owner settings
- OpenAI API for consultation answers, owner-style reasoning, escalation detection, and owner briefs
- Exa API only when useful for public enrichment or external context
- Optional lightweight agentic loop: answer, check escalation rules, identify knowledge gaps, then draft owner brief
- No production auth
- No Stripe
- No WhatsApp/Gmail/accounting integrations
