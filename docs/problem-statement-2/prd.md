# PRD: AI Digital Twin for SME Owners

## 1. Product Summary

Working name: Zo Expert

One-liner:

> Help SME owners stop losing leads and cash by turning customer threads into open-loop follow-ups, owner-style drafts, and a daily action brief.

## 2. Target User

Primary user:

- Small SME owner-operators.
- Roughly $0-$1M annual revenue.
- Strongest beachhead: S$100k-S$750k annual revenue.
- 1-8 staff.
- Owner still handles WhatsApp, email, calls, customer follow-ups, bookings, and payment chasing.

## 3. JTBD

When my business is growing but every customer reply, follow-up, booking, and payment reminder still depends on me, help me turn the way I run the business into an AI operator, so I can stop losing leads, cash, and control when I am busy.

## 4. Problem

Small business owners are the router, memory, and decision engine of the business. Leads, quotes, bookings, payments, and staff questions often fall through cracks because the owner is busy serving customers or doing delivery work.

## 5. MVP Scope

Build a localhost demo for an **AI Owner Follow-Up Desk**.

Core flow:

1. Owner enters business profile and operating rules.
2. App loads seeded customer/message threads.
3. App detects open loops.
4. App classifies each thread by urgency and revenue impact.
5. App drafts owner-style replies.
6. App generates a daily owner brief.

## 6. Core Features

- Owner/business profile
- Business rules and tone settings
- Mock WhatsApp/email-style inbox
- Open-loop detection
- Lead, quote, booking, payment, and approval classification
- Revenue-at-risk summary
- Owner daily brief
- Draft reply generator
- Approve/edit/ignore states

## 7. Non-Goals

- Real WhatsApp integration
- Real payment collection
- Full CRM
- Full accounting integration
- Multi-user permissions
- Fully autonomous sending
- Enterprise workflow automation

## 8. User Stories

- As an SME owner, I want to see which customer threads need action today.
- As an SME owner, I want the app to identify hot leads, stale quotes, and overdue payments.
- As an SME owner, I want replies drafted in my business tone.
- As an SME owner, I want to approve messages before they go out.
- As an SME owner, I want to see revenue at risk so I know what to prioritize.

## 9. Demo Data

Seed sample:

- Business type: appointment-led service business.
- Example verticals: renovation, beauty/wellness, tuition, clinic, home service, agency.
- Threads:
  - new lead asking for price
  - stale quote after 5 days
  - appointment reschedule request
  - overdue invoice
  - repeat customer asking FAQ
  - staff asking for decision

## 10. Success Metrics

Hackathon demo success:

- Can explain the target SME owner in under 20 seconds.
- Can show a messy inbox turning into prioritized open loops.
- Can show revenue at risk.
- Can show owner-style replies and approval flow.
- Can show why this is not a generic chatbot.

Product validation metrics:

- Owner identifies at least one real missed lead/payment/follow-up pattern.
- Owner says the daily brief would save time or recover revenue.
- Owner would pay weekly/monthly for open-loop tracking.

## 11. Open Questions

- Which vertical should be the first demo: home services, beauty/wellness, tuition, clinic, or agency?
- Should the first wedge be missed leads, stale quotes, or overdue payments?
- What level of automation feels safe to owners?
- Should pricing be per active conversation, per business, or tiered by monthly message volume?

## 12. Localhost Tech Stack Placeholder

TBD after build decision.

Likely fast path:

- Next.js or Vite React
- Local JSON seed data
- SQLite or localStorage
- OpenAI API for classification, summaries, and draft replies
- No production auth
