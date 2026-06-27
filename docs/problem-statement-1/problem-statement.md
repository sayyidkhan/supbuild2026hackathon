# Problem Statement 1 Idea: Relationship Trust-Path Mapper

## Problem statement link

Original direction:

> Trust, Commerce & Fraud... Build systems that make online transactions safer, reduce scams, detect fraud, and increase trust in digital marketplaces.

Founder reinterpretation:

This can link into Future of Work if we treat work opportunities as trust-driven transactions. Hiring, freelancing, partnerships, mentoring, fundraising, customer discovery, and collaborations all depend on trust. AI makes profiles, applications, portfolios, and outreach cheaper to generate, so warm trusted paths become more valuable.

## Idea

A relationship intelligence app that helps people map the fastest credible trust path to a work opportunity.

This is not a career coach. It is not another resume tool. It is not a generic personal CRM.

Primary beachhead: working professionals with 5-20 years of experience who already have enough career history, projects, companies, colleagues, communities, and achievements for the system to find useful opportunity paths. They also have enough income and urgency to pay for a SaaS product that improves career leverage.

It helps a user answer:

- Who do I know who can help me access this opportunity?
- Who knows the person, company, hiring manager, team, recruiter, industry operator, or community I want to reach?
- Which relationship path has the strongest trust context?
- What should I ask for next: intro, advice, feedback, referral, collaboration, or warm conversation?

## JTBD framing

When I find a high-value career opportunity but I do not have obvious access, help me map the fastest credible trust path through my real career history and relationships, so I can make a warm and contextual move instead of relying on cold applications or generic outreach.

## User POV

I have people scattered across LinkedIn, Telegram, WhatsApp, GitHub, past companies, schools, communities, conferences, projects, and professional circles.

When I need to reach a company, hiring manager, recruiter, senior operator, mentor, or collaborator, I do not know which relationship path is strongest. I also do not know what to say or whether I should ask for an intro, reconnect first, or show proof of work.

I need a system that turns my career history and fragmented network into actionable opportunity paths.

## Struggling moment

The user has a target but no obvious route.

Examples:

- I want to reach a hiring manager at a company.
- I want to move from my current company into a better role.
- I want to explore a startup, operator, advisory, or fractional opportunity.
- I want to reach someone senior in a target industry.
- I want to reconnect with past colleagues who can open doors.
- I met many people at conferences, hackathons, or professional events but do not know who to follow up with.
- I need a warm path into a role, company, community, collaboration, or side opportunity.

## Target users

Primary target:

- Working professionals with meaningful career history and buying power.
- Mid-career and senior professionals with roughly 5-20 years of experience.
- Likely age range: 28-45 years old.
- Strongest beachhead: 30-42 years old with 7-15 years of experience.
- Professionals who have worked across multiple companies, projects, teams, communities, or industries.
- Professionals who are not entry-level and have enough "meat" in their resume for the app to mine useful relationship and opportunity signals.

Why career stage matters more than age:

- 5 years of experience usually means the person has enough work history, former colleagues, projects, and industry context to map useful opportunity paths.
- 7-15 years of experience is the strongest wedge because the user has stronger buying power, active career ambition, and a network they are likely underusing.
- 15-20 years of experience can work for senior, advisory, fractional, board, consulting, and executive opportunities, but the product may need a more premium positioning.
- Age is useful for rough segmentation, but positioning should lead with career stage and opportunity access.

Likely early adopter profiles:

- Software engineers exploring better roles, startups, consulting, or fractional work.
- Product, ops, strategy, and business professionals looking for higher-leverage opportunities.
- Ex-consultants, ex-bankers, and ex-corporate operators with broad networks.
- Professionals transitioning from employee to founder, freelancer, consultant, or operator.
- Senior individual contributors and managers who know their next opportunity is likely relationship-driven.

Why this target:

- They already have a meaningful network.
- They have resume depth, project history, and company history that can produce useful signals.
- They feel the pain of opportunity access and career leverage.
- They are more likely to pay for a SaaS product than students, junior jobseekers, or casual networkers.
- They want better opportunities, not generic career advice.

Secondary targets later:

- Founders
- Freelancers and consultants
- Hackathon builders
- Community-driven builders
- Startup ecosystem operators

## Existing behavior and workarounds

Users currently use:

- LinkedIn search
- Manual memory
- Notes apps
- Spreadsheets
- Telegram and WhatsApp history
- GitHub profiles
- Event attendee lists
- Resume and LinkedIn profile exports
- Past company alumni networks
- Personal CRM tools
- Asking friends manually
- Cold applications and cold outreach

These fail because they track contacts, not opportunity-specific trust paths.

## Market awareness

Adjacent product categories already exist:

- Personal CRM: Dex, Clay, folk, Monica
- Relationship intelligence CRM: Affinity, Introhive
- Sales and warm-intro tooling: LinkedIn Sales Navigator, Connect The Dots
- Fundraising relationship tools: investor CRM and intro-path products

The weak version of this idea is already crowded:

> Map my contacts and remind me to keep in touch.

The sharper wedge is:

> Given a working professional's resume, career history, and relationship context, rank the best trust paths and next actions for a specific career opportunity.

## Differentiation

Focus on opportunity access, not contact management.

The app should be:

- Career-context-first: use the user's resume, LinkedIn-style profile, past companies, projects, and communities as the base graph.
- Target-first: start with a person, company, role, team, recruiter, industry, opportunity, or community.
- Relationship-aware: rank paths by relationship strength and context.
- Proof-of-work-aware: connect relationship paths to actual projects, commits, demos, writing, achievements, roles, and past work.
- Action-oriented: recommend the next move, not just show a graph.
- Career-leverage-native: useful during job changes, internal mobility, founder transitions, consulting pivots, and professional repositioning.

## MVP demo flow

1. User enters a target: person, company, role, team, or opportunity.
2. User uploads or enters career context:
   - resume
   - LinkedIn-style profile
   - past companies
   - roles and projects
   - communities and events
   - skills and achievements
3. App uses Exa to find public LinkedIn/person/company pages related to the target.
4. App extracts candidate people and relationship signals:
   - name
   - company
   - role
   - hiring proximity
   - shared company
   - shared community
   - shared domain
   - proof-of-work relevance
5. App builds a public relationship and career-context graph.
6. App ranks trust paths:
   - direct connection
   - shared company
   - shared school, community, or event
   - shared project
   - mutual connection
   - alumni overlap
   - career relevance
7. App recommends the best next action:
   - ask for intro
   - reconnect first
   - send proof-of-work update
   - ask for advice
   - request referral
   - invite to collaborate
8. App generates a contextual message that does not feel like spam.

## Demo style

Use a two-layer demo:

1. HyperFrames for the external demo video.
2. Driver.js for guided in-app onboarding.

HyperFrames should produce a short 45-75 second product demo that can be used in the hackathon pitch, landing page, README, or async judging flow. The story should be:

> Paste profile -> enter target opportunity -> discover public people/company signals -> rank trust paths -> generate warm outreach -> mark next action.

Driver.js should guide the user inside the live app after they open it. The tour should be action-driven, not a passive click-through:

1. Paste or load the seeded profile.
2. Confirm the target opportunity.
3. Run discovery.
4. Inspect discovered people.
5. Rank trust paths.
6. Select the best path.
7. Generate outreach and update the outcome.

The HyperFrames video explains value before signup or judging. The Driver.js tour drives activation inside the product. Both should reuse the same seeded persona, target, and success narrative so the demo feels coherent.

## Possible hackathon scope

Do not depend on direct LinkedIn scraping, LinkedIn OAuth, Gmail, contacts sync, or payment integrations. Use Exa to discover public LinkedIn/person/company pages for the proof of concept.

Build a working prototype with:

- Seeded demo dataset
- Resume upload or paste-in profile parser
- Exa-powered people/company discovery
- Simple contact and opportunity form
- Graph visualization
- Trust-path ranking
- AI-generated next-action suggestions
- Message draft generation

Nice-to-have if time allows:

- GitHub profile/project enrichment
- LinkedIn-style profile import from pasted text or exported PDF
- Relationship history timeline

## Data model sketch

Entities:

- Person
- Organization
- Opportunity
- Relationship
- Interaction
- Project or proof-of-work
- Community or event
- Resume item
- Role
- Skill

Relationship attributes:

- source
- strength
- recency
- context
- mutual contacts
- shared affiliation
- trust reason
- opportunity relevance
- career relevance

## Trust score sketch

Trust path score could combine:

- relationship strength
- recency of interaction
- relevance to target
- shared affiliation
- proof-of-work match
- career-history match
- number of hops
- confidence of data
- actionability

Avoid pretending this score is objective. Present it as decision support.

## Research questions

For online market research, look for evidence around:

- How do mid-career professionals currently get warm referrals?
- How do working professionals decide who to reconnect with when exploring a move?
- What frustrates users about personal CRM tools?
- What makes people trust a referral?
- Where do warm-intro tools fail?
- How do recruiters and hiring managers evaluate referrals compared with cold applicants?
- How do professionals use alumni networks, past colleagues, and communities to access opportunities?
- How do professionals manage weak ties over long career arcs?

Useful search targets:

- Reddit threads about personal CRM pain
- Hacker News discussions about networking tools
- LinkedIn posts about warm intros and job referrals
- G2 reviews for personal CRM and relationship intelligence tools
- Jobseeker posts about referrals and cold applications
- Mid-career transition posts
- Alumni network and professional networking discussions

## Risks

- Too generic if positioned as a personal CRM.
- Too generic if positioned as a job-search or career-coach tool.
- Too hard if it requires full contact import integrations during the hackathon.
- Privacy concerns if users feel the app is exploiting their network.
- Weak demo if the graph looks cool but does not recommend a concrete next action.
- Direct LinkedIn scraping or LinkedIn API dependency could break or violate platform constraints; use Exa public search instead.
- Weak willingness to pay if targeting students or entry-level jobseekers instead of working professionals.

## Better positioning

Weak:

> AI networking app.

Better:

> A trust-path engine for opportunity access.

Stronger:

> Turn a working professional's resume, relationships, and proof-of-work into warm paths for better roles, collaborators, mentors, and career opportunities.

## Hackathon narrative

AI has made applications, messages, resumes, and portfolios cheap to generate. The scarce asset is no longer polished content. The scarce asset is trust.

Future work opportunities will increasingly flow through communities, proof-of-work, reputation, and warm relationship paths. This tool helps working professionals see and activate those paths.

It fits Problem Statement 1 because it builds trust infrastructure.

It also fits Future of Work because it helps working professionals access better opportunities through trusted relationships instead of noisy cold application funnels.

## Open decision

The first target user is now:

> Mid-career and senior working professionals with 5-20 years of experience, roughly aged 28-45, with the strongest beachhead around 30-42 and 7-15 years of experience.

Need to decide which working-professional segment is narrowest for the first prototype:

- software engineers exploring better roles or startup opportunities
- consultants/bankers/corporate operators exploring operator or founder paths
- mid-career professionals trying to switch industry or function
- senior ICs/managers trying to activate weak ties for hidden opportunities

For the hackathon, the strongest demo may be:

> Resume-to-trust-path mapper for working professionals.

This keeps the scope concrete, monetizable, and aligned with a user who can pay.
