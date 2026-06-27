# PRD: Relationship Trust-Path Mapper

## 1. Product Summary

Working name: Zo Relationship Mapper

One-liner:

> Before applying cold, help mid-career professionals use Exa-powered LinkedIn/person discovery to find the highest-trust path into a target role, company, or opportunity.

## 2. Target User

Primary user:

- Mid-career and senior working professionals.
- 5-20 years of experience.
- Strongest beachhead: 30-42 years old, 7-15 years of experience.
- Has enough career history, network density, and willingness to pay for career leverage.

## 3. JTBD

When I find a high-value career opportunity but do not have obvious access, help me map the fastest credible trust path through my real career history and relationships, so I can make a warm, contextual move instead of relying on cold applications.

## 4. Problem

Cold applications are noisy and low-trust. Mid-career professionals often have useful weak ties, alumni connections, ex-colleagues, and community relationships, but they do not know which path is most credible for a specific opportunity.

## 5. MVP Scope

Build a localhost demo for a **Trust Path Sprint**.

Implementation goal brief: [goal.md](./goal.md)

Core flow:

1. User enters career profile or uploads/pastes resume text.
2. User adds target company, role, person, or opportunity.
3. App uses Exa to find relevant public LinkedIn/person/company pages.
4. App uses OpenAI to compare discovered people against the user's resume, career history, and target.
5. App ranks best trust paths and explains why each person is relevant.
6. App recommends next action and drafts outreach.
7. App tracks outcome state.

## 6. Core Features

- Career profile input
- Target opportunity input
- Exa-powered LinkedIn/person discovery
- Public company/person enrichment
- Trust path ranking
- Path explanation
- Next-best-action recommendation
- Contextual message draft
- Follow-up tracker

## 7. Non-Goals

- Full CRM
- Direct LinkedIn scraping or LinkedIn API dependency
- Gmail, Google Contacts, Microsoft Graph, or other OAuth-heavy integrations
- Stripe or payment integration
- Automated outreach
- Real email sending
- Full job application tracker
- Career coaching chatbot

## 8. User Stories

- As a mid-career professional, I want to paste my resume so the app can understand my career context.
- As a user, I want to enter a target company or role so I can find warm paths before applying.
- As a user, I want to see why a relationship path is credible so I can decide whom to contact.
- As a user, I want a message draft that sounds contextual and not spammy.
- As a user, I want to track whether a path resulted in advice, referral, intro, no response, or dead end.

## 9. Demo Data

Seed sample:

- User profile: mid-career software/AI professional.
- Target: startup/operator role, AI company, or sustainability tech company.
- Exa results: public LinkedIn/person pages, company pages, hiring managers, recruiters, founders, team leads.
- Relationship signals: shared company, shared community, shared project, shared domain, role relevance, hiring proximity.

## 10. Demo Style

Use two demo layers:

- HyperFrames for the external product demo video used in the hackathon pitch, landing page, README, or async judging flow.
- Driver.js for guided in-app onboarding after the user opens the live product.

The demo narrative should be consistent across both:

> Paste profile -> enter target opportunity -> discover people/company signals -> rank trust paths -> generate outreach -> mark contacted.

The in-app Driver.js tour should make the user perform the core workflow, not just read tooltips.

## 11. Success Metrics

Hackathon demo success:

- Can explain the target user in under 20 seconds.
- Can show a target opportunity turning into ranked trust paths.
- Can show a concrete next action and outreach draft.
- Can show why this is not a generic CRM.
- Can show the same seeded workflow through both a video demo and in-app guided tour.

Product validation metrics:

- User sends at least one suggested outreach.
- User gets a reply, advice call, referral, or intro.
- User would pay for a 30-day Trust Path Sprint.

## 12. Open Questions

- Should the first target be tech professionals, consultants, finance professionals, or operators?
- Should pricing be monthly SaaS or sprint-based?
- What minimum profile and target data is enough for a useful Exa-powered path map?
- How should trust scores be explained without feeling creepy?

## 13. API Constraints

Use only:

- OpenAI API
- Exa API
- Local seed data / browser storage

Do not use:

- Stripe
- Gmail/Google Contacts
- Microsoft Graph
- LinkedIn API
- Direct LinkedIn scraping

## 14. Localhost Tech Stack

Detailed stack: [tech-stack.md](./tech-stack.md)

Localhost-only fast path:

- Vite + React
- TanStack Router if routing is needed
- TanStack Query for API calls/state around Exa/OpenAI requests
- Local JSON seed data for fallback demo state
- Browser localStorage for saved targets/outcomes
- OpenAI API for resume parsing, fit reasoning, trust-path ranking, and message drafts
- Exa API for public LinkedIn/person/company discovery
- Driver.js for guided in-app onboarding
- HyperFrames for external demo video generation/storyboard
- No production auth
- No Stripe
- No Gmail/contacts integrations
