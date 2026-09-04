# Datavant Working Profile

_Last updated: August 31_ 2026_

This document is a self-contained working profile of Datavant, onboarding context, Routing team observations, people profiles and current organizational hypotheses. It is intended to be uploaded into a new ChatGPT conversation so the work can continue without rebuilding context.

## 8. Datavant Organizational Context

### Business / organizational signals from Week 1

From Ryan and team notes:

- Company had a reveal in the 7+5 forecast
- Payer is positive but below plan
- All-team meetings were cut
- Most open headcount was closed
- Only four IC roles were approved as exceptions
- Provider reportedly had 18 roles open and 16 were closed
- Security hiring was postponed
- Life Sciences had a major relocation to Barcelona several months earlier
- Team members carried baggage from organizational changes
- There has been repeated leadership turnover
- Delivery pressure and customer renewal pressure are meaningful
- Timeline commitments have sometimes occurred before Engineering discovery

### Working organizational hypothesis

**This is not yet considered a confirmed fact.**

Current hypothesis:

> Datavant appears to be operating in a more financially disciplined, transaction-ready mode than a culture-building mode. Leadership appears focused on efficiency, predictability, customer retention and near-term execution. The team is feeling the effects through reduced headcount, higher delivery pressure, leadership churn and less investment in engineering health.

Possible explanation:

- leadership may be preparing the company for a sale, IPO or other liquidity event

Evidence supporting the hypothesis:

- cost and headcount controls
- changes in leadership, compensation and equity
- reduced cultural investment
- revenue / renewal pressure
- employees describing a decline from an older engineering culture
- strong emphasis on execution and predictability

This should remain a hypothesis until senior leadership messaging or other evidence confirms it.

---

## 9. Current Team: Routing

Manager: **Ryan Ma**

Direct reports:

- **Kevin Li, P3**
- **Magaly Gutierrez, P3**
- **Vince Herr, Staff Engineer**

Product Manager:

- **Connor**

Recent interim EM:

- **Tim Song**

### Team summary after Week 1

The Routing team appears technically capable and committed, but is operating under a reactive and fragile model.

Main patterns:

- high support load
- constant interruptions
- too many high-priority items
- weak WIP control
- insufficient feature work
- knowledge heavily concentrated in Vince
- poor onboarding
- fragmented documentation
- unclear / inconsistent Product and Engineering prioritization
- support requests bypassing clear intake
- DLQ instability and hard-to-understand async message flows
- repeated leadership changes
- retention risk
- process maturity improving because of Tim’s interim work

### High-level team health

| Area | Current assessment |
|---|---|
| Technical capability | Good |
| Team relationships | Generally good |
| Knowledge distribution | Poor |
| Support load | Very high |
| Focus / WIP control | Poor |
| Onboarding | Poor |
| Product / Eng alignment | Inconsistent |
| Process maturity | Improving |
| Documentation | Inadequate but improving |
| Retention risk | Meaningful |
| Biggest dependency | Vince |
| Biggest systemic issue | Reactive support + fragmented knowledge |

### Systemic loop

High support load  
→ constant interruption  
→ insufficient feature / system work  
→ insufficient documentation  
→ dependency on Vince  
→ poor onboarding  
→ lower independent capability  
→ more dependency on Vince  
→ even more interruption

A second loop:

Weak intake / prioritization  
→ too much WIP  
→ shallow investigation  
→ recurring support problems  
→ Product loses predictability  
→ more urgency and priority changes

### Baseline conclusion

> Routing is a capable team trapped in a reactive operating model. The immediate management problem is not motivation or raw engineering ability. It is stabilizing intake and priorities, reducing support pressure, distributing Vince’s knowledge and creating enough space for Kevin and Magaly to develop deeper ownership.

---

## 10. Systems and Technical Context

### Products / systems

- New system: **Switchboard**
- Legacy data model: **IDSB**
- Member Locator
- Provider Locator
- traditional retrieval pipelines
- information request flows
- member / provider retrieval
- async / queue-driven architecture
- approximately 30 to 40+ queues
- DLQs are a major reliability problem

### Team architecture / reliability problems

Routing sits centrally between Switchboard and retrieval sources.

Current issues:

- DLQ growth
- stalled request inventory
- state syncing issues
- difficult root-cause analysis
- reroute requests
- support-driven queue work
- low environment confidence
- testing is difficult because there is no meaningful lower environment
- some testing occurs in production
- difficult to understand where inventory is
- root problems often relate to matching and data foundations

### Support

Support consumes significant team capacity.

Common support work:

- rerouting inventory between retrieval methods
- updating addresses / phone information
- queue investigation
- Member Locator incidents
- internal requests
- client / operations escalations

Tim’s proposed direction:

- offload repeatable requests to a new Support team
- build runbooks
- improve formal intake
- retain Member Locator as a special case until documentation and ownership are clearer

---

## 11. Tim Song’s Interim Assessment

Source file: **Routing Proposals.pdf**

Tim’s high-level north star:

- make the team self-sustaining
- distribute knowledge
- make onboarding repeatable
- create shared Product / Engineering prioritization
- build clear intake and visibility
- make system reliability a first-class investment

His four major opportunity areas:

1. Culture of shared ownership
2. DLQ stability
3. Large support-request volume
4. Engineering and Product alignment

### Proposed allocation model

- 60% Product work
- 30% Engineering + Security investment
- 10% Support + KTLO

### Proposed process

1. Product kickoff with PRD / why
2. Owning engineer creates one-pager / spike
3. Team reviews approach
4. Continuous planning and refinement

Tim’s work is a useful starting hypothesis, not something to inherit blindly.

---

## 12. People Profiles

### Ryan Ma — Manager

Initial read:

- understands the team’s structural problems
- knows Vince is a major single point of failure
- wants support limited to roughly two engineers where possible
- concerned about execution capacity
- aware of leadership churn
- operating under organizational cost constraints
- may value a manager who stabilizes the team without requiring constant intervention

Relevant context:

- headcount restrictions are real
- hiring may not be an easy solution
- several approved hiring exceptions exist
- Payer is under performance pressure

---

### Kevin Li — P3

**Important correction:** Kevin is currently a **P3**, not P4.

He had previously been expected to move to P4, but organizational changes disrupted that path.

#### Strengths

- strong engineer
- curious
- willing to dive deeply into hard problems
- confident technical problem solver
- mentoring capability
- technical process leadership
- collaborative
- willing to challenge assumptions
- good teammate
- learns from Vince
- has helped junior engineers triage on-call issues
- has handled difficult bug investigations

#### Frustrations / risks

- too much support work
- too many simultaneous high-priority items
- regular context switching
- feature work repeatedly displaced
- difficulty identifying what is actually going well in the work
- possible retention risk
- historical frustration around promotion and compensation
- current system dependency on Vince limits autonomy

#### Career direction

- prefers product / feature work
- wants to grow
- wants clear milestones
- wants feedback on whether he is actually doing well
- prior feedback suggested stronger relationships across teams

#### Management plan

**Primary development objective: help Kevin reach P4.**

This should be a recurring part of 1:1s:

- define concrete P4 expectations
- identify evidence he already has
- identify actual gaps
- create opportunities for broader ownership
- strengthen cross-team influence
- track milestones
- make promotion readiness explicit rather than ambiguous

This is also an early measurable people-leadership objective for the manager.

---

### Magaly Gutierrez — P3

#### Background

- Engineer for about 7 years
- Approximately 6 years at Capital One
- Joined Datavant / Life Sciences in April 2025
- Joined Payer in June 2026
- background includes Mexico, Alabama, Boston and New York

#### Strengths

- positive influence
- creative
- passionate
- willing to learn
- documentation-oriented
- working on logging improvements
- using AI to help understand code and documentation
- appreciates retros, standups and public-channel communication
- interested in improving support
- collaborative

#### Development areas

- needs clearer acceptance criteria
- needs more guidance when work is ambiguous
- independent investigation depth
- understanding system context
- asking the right questions
- validating AI-generated work
- operating confidently in high-pressure support
- needs progressively more ownership

#### Current dynamic

Magaly feels bad pulling Vince into too much support because he is the only deep SME.

She wants:

- more feature work
- less support
- more time learning from Vince

#### Vince’s view

Vince’s assessment is significantly harsher:

- needs substantial hand-holding
- not asking enough of the right questions
- may rely too heavily on AI
- output quality is not always sufficient
- could struggle in crunch situations

This should be treated as **one data point**, not the final performance assessment.

#### Management approach

Use explicit expectations and progressive ownership to distinguish:

- normal P3 development needs
- domain knowledge gaps
- actual performance gaps

---

### Vince Herr — Staff Engineer

#### Role in the team

Vince is currently the most important technical dependency.

He holds:

- original Routing context
- substantial Member Locator context
- historical engineering knowledge
- system architecture understanding

#### Strengths

- very strong technical judgment
- deep domain knowledge
- high ownership
- willingness to teach
- strong historical perspective
- ability to quickly judge quality
- trusted by Ryan
- frequently consulted by engineers and stakeholders

#### Risks

- major bottleneck
- single point of failure
- burnout risk
- too many direct pings
- too much review demand
- support interruptions
- de facto technical management
- difficulty letting go when he does not trust others’ understanding
- frustration with shallow technical understanding
- frustration with low-quality AI output

#### Cultural perspective

Vince remembers an older engineering culture that he viewed as much stronger.

He sees:

- leadership changes
- comp changes
- equity changes
- two different engineering cultures
- newer people who tend to just do assigned work
- reduced depth of technical understanding
- culture erosion

#### Management need

The goal is **not** to diminish Vince’s importance.

The goal is to:

- protect his time
- deliberately extract / distribute knowledge
- create trusted secondary owners
- document critical systems
- reduce unnecessary pings
- let him focus on Staff-level leverage
- make him less operationally necessary without making him feel less valued

---

### Connor — Product Manager

#### Initial read

Connor appears well-intentioned and under pressure.

Positive signals:

- trying to protect engineers from stakeholders
- good at creating tickets
- recognizes the team is too support-focused
- recognizes Vince as a risk
- wants feature and tech-debt work

Problems in the current Product / Engineering interface:

- support triage is inconsistent
- tickets sometimes get grouped incorrectly
- work sometimes goes directly to engineers
- engineers do not always understand the “why”
- Product lacks enough system context
- combining tickets can block root-cause analysis
- engineering commitments sometimes happen before discovery

#### Management relationship goal

Move toward:

- joint prioritization
- shared engineering / product visibility
- explicit tradeoffs
- better intake
- fewer hidden priorities
- clearer understanding of business importance

Connor should not be viewed as “the problem.” He appears to be trying to shield engineering without enough domain context or a mature operating system.

---

### Tim Song — Interim EM

Tim stabilized several things before the new EM arrived.

Contributions:

- brought back refinement
- brought back retros
- improved board visibility
- improved intake thinking
- created written team assessment
- started knowledge transfer
- highlighted DLQ stability
- highlighted support overload
- proposed Product / Engineering allocation guardrails

His assessment aligns closely with what the team independently reports, which gives it credibility.

---

## 13. Week 1 Conversations

Completed 1:1s / discovery conversations with:

- Ryan Ma
- Kevin Li
- Magaly Gutierrez
- Vince Herr
- Connor
- Tim Song

Additional artifacts:

- Tim Song’s Routing assessment
- Routing proposals
- onboarding notes
- individual first 1:1 notes

### Week 1 purpose

Treat initial conversations as discovery, not judgment.

Goal:

- understand official process versus actual process
- identify hidden work
- learn where work slows down
- identify interruption patterns
- understand leadership expectations
- establish initial people / team hypotheses

---

## 14. Immediate Management Priorities

Current likely priorities:

1. Stabilize intake and prioritization
2. Reduce total WIP
3. Protect the team from constant support interruption
4. Reduce Vince as the only viable SME
5. Build technical documentation
6. Improve onboarding
7. Clarify DLQ ownership / reliability work
8. Build Product / Engineering operating trust
9. Help Kevin build a concrete P4 path
10. Give Magaly structured opportunities for deeper ownership
11. Protect Vince from burnout
12. Validate which parts of Tim’s process changes are actually helping

---

## 15. Open Questions to Validate

### Organization

- Is Datavant explicitly preparing for an IPO, sale or other liquidity event?
- What are executive incentives?
- What does senior leadership emphasize most:
  - growth
  - margin
  - EBITDA
  - efficiency
  - predictability
  - customer retention
  - transaction readiness
- How permanent are current headcount controls?

### Routing

- Actual support volume by week
- Percentage of capacity consumed by support
- Number of active priorities at one time
- Which workstreams are actually highest business value
- Current ownership map
- systems only Vince can reliably support
- existing documentation quality
- DLQ root causes
- how much support work can move to Support team
- Member Locator ownership future
- how much of Tim’s 60/30/10 framework is actually being followed

### Kevin

- Exact P4 expectations
- prior promotion packet / evidence
- current gaps
- compensation constraints
- retention timeline

### Magaly

- Where guidance is actually needed versus where expectations are unclear
- ability to independently own a scoped feature
- ability to debug without Vince
- AI validation habits
- support-readiness

### Vince

- burnout level
- retention risk
- areas he wants to stop owning
- areas he wants to continue owning
- realistic knowledge-transfer plan
- Staff-level work he is currently unable to do because of interruptions

### Equity

- exact RSU grant agreement
- Odyssey TopCo equity plan
- change-of-control treatment
- IPO treatment
- accelerated vesting terms
- post-termination treatment
- current share valuation mechanics
- liquidity options before IPO
- stock split / recapitalization language

---

## 16. Current Working Conclusions

### Compensation

Datavant is a very strong guaranteed-cash offer at $265,000 base, even before equity.

### Equity

The 500 RSUs could be very valuable, but should not be treated as spendable compensation until vested and liquid.

### Team

The team is not fundamentally dysfunctional. The system around them is.

### Culture

There are credible signs of culture erosion and increased business / transaction pressure.

### Leadership opportunity

The strongest opportunity is to turn a reactive, SME-dependent team into a stable team with:

- explicit priorities
- controlled support
- shared ownership
- repeatable onboarding
- stronger product alignment
- distributed technical knowledge
- visible engineer growth

That creates measurable management impact even if the broader company remains financially or transaction focused.

---

## Source Files Used

- Datavant2026BenefitsGuide.pdf
- Kevin Li Initial 1 on 1.pdf
- Magaly Gutierrez Initial 1 on 1.pdf
- Vince Herr Initial 1 on 1.pdf
- Onboarding Notes.pdf
- Routing Proposals.pdf
