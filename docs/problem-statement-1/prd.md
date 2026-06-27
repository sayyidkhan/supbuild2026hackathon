# PRD: Relationship Trust-Path Mapper

## 1. Product Summary

Working name: Zo Relationship Mapper

One-liner:

> Before applying cold, help mid-career professionals find the highest-trust path into a target role, company, or opportunity.

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

Core flow:

1. User enters career profile or uploads/pastes resume text.
2. User adds target company, role, person, or opportunity.
3. User imports or uses seeded relationship data.
4. App ranks best trust paths.
5. App recommends next action and drafts outreach.
6. App tracks outcome state.

## 6. Core Features

- Career profile input
- Target opportunity input
- Seeded/manual contact graph
- Trust path ranking
- Path explanation
- Next-best-action recommendation
- Contextual message draft
- Follow-up tracker

## 7. Non-Goals

- Full CRM
- LinkedIn scraping
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
- Contacts: ex-colleagues, alumni, hackathon contacts, community members, recruiters.
- Relationship paths: direct, second-degree, shared company, shared community, shared project.

## 10. Success Metrics

Hackathon demo success:

- Can explain the target user in under 20 seconds.
- Can show a target opportunity turning into ranked trust paths.
- Can show a concrete next action and outreach draft.
- Can show why this is not a generic CRM.

Product validation metrics:

- User sends at least one suggested outreach.
- User gets a reply, advice call, referral, or intro.
- User would pay for a 30-day Trust Path Sprint.

## 11. Open Questions

- Should the first target be tech professionals, consultants, finance professionals, or operators?
- Should pricing be monthly SaaS or sprint-based?
- What minimum imported data is enough for a useful path map?
- How should trust scores be explained without feeling creepy?

## 12. Localhost Tech Stack Placeholder

TBD after build decision.

Likely fast path:

- Next.js or Vite React
- Local JSON seed data
- SQLite or localStorage
- OpenAI API for ranking/explanations/message drafts
- No production auth
