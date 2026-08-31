# Datavant Work Context Summary

_Last updated: August 31, 2026_

This file is meant to carry forward the **work context only** for Datavant conversations. It intentionally excludes interview history, offer details, compensation, benefits and job-search context.

---

## 1. Current Role Context

You are leading the **Payer Routing** team at Datavant. The team sits in a critical part of the Payer/Switchboard area and appears to own or influence routing, rerouting, retrieval workflows, record request movement and several support-heavy operational paths.

The broader context is that Routing is viewed as a high-value, high-risk part of the business. Senior engineering leadership has described the pod as important to the core IP of Switchboard and one of the biggest leverage points in the business. The team is also seen as fragile because of concentrated knowledge, reactive support load, unclear capacity and a history of weak management structure.

Current working interpretation:

> Routing is a capable team trapped in a reactive operating model. The immediate problem is not motivation or raw engineering ability. The problem is stabilizing intake and priorities, reducing support pressure, distributing Vince’s knowledge and creating enough space for the team to develop deeper ownership.

---

## 2. Current Team and People Context

### Ryan Ma

Ryan is your manager and owns broader responsibility for the area. He has strong Datavant context and understands the historical complexity of the systems and people. He appears to recognize that Routing has not simply had a capacity problem. It has a context, system-health and operating-model problem.

Ryan’s recent framing:

- Routing has had multiple load-balancing attempts with temporary engineers.
- Temporary capacity has not solved the problem because contextless ICs do not automatically become Routing capacity.
- The team has carried more burden as people have left and support/features have bottlenecked through Routing.
- Vince and Ryan have pushed back on adding people when those people do not have enough SME context.
- Product may perceive Routing as unwilling to accept help, while Engineering sees the issue as help that does not actually reduce load.
- Continuing to push support tickets and client features means the team is accepting a degraded system state.
- Reroutes was an example where automation/self-service was being pushed before the underlying scripts and system reliability were ready.

Current read:

> Ryan is opening the door for a more mature operating-model discussion. He is not just saying “Routing is overloaded.” He is saying the old answer of “add ICs” has not worked, and the team needs a better model for effective capacity.

### Vince Herr

Vince is the primary Staff Engineer and the deepest remaining Routing SME. He is a major concentration risk, especially around historical context, Member Locator and complicated rerouting/retrieval behavior.

Strengths:

- Deep system knowledge.
- Strong technical judgment.
- High ownership.
- Valid concerns about system correctness, scripts, data integrity and support-driven work.
- People learn a lot from him when they are in the room with him.

Concerns:

- Knowledge remains concentrated around him.
- He prefers building/fixing over enabling others.
- He has said he likes letting people learn for themselves.
- That approach is not working well in Routing because the system is complex, documentation is weak and support pressure is high.
- His frustration may be legitimate, but his current operating model may reinforce dependency.
- Senior leadership may already perceive the pattern as more than normal pushback.

Working distinction:

> Vince clearly has Staff-level system knowledge and technical judgment. The open question is whether his current operating mode is creating Staff-level leverage or reinforcing Staff-level dependency.

The Datavant IC ladder says organizational impact is part of everyone’s role and includes knowledge transfer, documenting workflows, mentoring, pair programming and continuous improvement. For P5 Staff Engineers, the ladder describes the primary distinction from P4 as scope and complexity of impact, often across multiple pods or a whole vertical. A P5 is expected to be a go-to person for system knowledge, design decisions, team interfaces and improvement ideas while still delivering high-quality individual contribution.

This creates a useful coaching frame:

> The goal is not to reduce Vince’s importance. The goal is to shift more of his effort into structured leverage: pairing, runbooks, decision logs, current-state docs, office hours and secondary ownership.

### Kevin Li

Kevin is a P3 and had previously been expected to move toward P4. Organizational changes disrupted that path.

Strengths:

- Strong engineer.
- Curious.
- Dives deeply into hard problems.
- Willing to challenge assumptions.
- Learns a lot from Vince.
- Has handled challenging bugs and technical process work.

Risks and needs:

- Wants clearer promotion milestones.
- Needs a deliberate P3-to-P4 growth path.
- May be a retention risk because of prior promo disruption and compensation ceiling concerns.
- Needs opportunities for broader ownership and cross-team relationships.

Working management plan:

> Helping Kevin reach P4 should be a recurring 1:1 and development priority. The work should be explicit: define P4 expectations, identify evidence he already has, identify gaps, create ownership opportunities and track progress.

### Magaly Gutierrez

Magaly is a P3 and newer to Payer/Routing.

Strengths:

- Positive influence.
- Creative and passionate.
- Willing to learn.
- Interested in documentation and logging improvements.
- Uses AI tools to help understand code and generate documentation.

Risks and needs:

- Needs clearer acceptance criteria.
- Needs more guidance when ambiguity is high.
- Needs to validate AI-generated outputs carefully.
- Needs structured ownership rather than being dropped into chaotic support.
- May be better suited to work where there is more clarity and guidance.

Working management plan:

> Give Magaly ownership, but in a structured way. She needs clear goals, strong acceptance criteria, defined escalation paths and focused areas where she can build confidence without becoming another dependency on Vince.

### Connor Feick

Connor is the PM for Routing. He joined during a period of leadership churn and has been trying to act as a buffer between stakeholders and engineers.

Observed strengths:

- Trying to protect engineering time.
- Creates tickets.
- Has helped improve public-channel communication.
- Has been involved in triage and prioritization.

Concerns:

- May not always have enough system or product context to make strong decisions.
- Sometimes groups support items together in ways that make root-cause analysis harder.
- Product-side documentation is weak.
- The team needs clearer product lifecycle docs, statuses and workflow diagrams.

Working relationship need:

> Connor needs a clearer partnership model with Engineering so PRDs, prioritization, support tradeoffs and current-state system limitations are understood before commitments are made.

### Sophie Gershon

Sophie is an EM in the broader zone and may move back toward an IC role.

Important context:

- Current cross-team collaboration is mostly EM-to-EM, while IC-to-IC collaboration has declined due to attrition and timing.
- Resource competition is causing friction.
- One of her engineers gave notice recently.
- She does not currently believe leadership is doing enough to address turnover.
- Her team has useful context, including front-end expertise, operational workflows, retrieval workbench and potentially work around a state-manager source of truth.

Potential implication:

> Sophie moving back to IC could be a catalyst for a short-term restructure or realignment of engineers across the zone.

### Abby Anmuth

Abby is Group PM over Data Foundations and Routing.

Important context from Abby:

- Chartfinder was inherited.
- The team decided to rebuild with more controls.
- Some decisions were made last year around MVP and migration scope.
- The consequences of not building certain features were underestimated.
- Manual handling was assumed to be manageable but turned out worse than expected.
- Inventory management is now difficult because of those manual pieces.
- There is a question of whether the difficulty is due to concentration risk around Vince or whether the work itself is harder than expected.
- There have been resources ready to help, but embedding people has repeatedly come up short.

Working interpretation:

> Some prior scope decisions converted missing product or system capability into recurring manual engineering support. This was a self-inflicted support burden, not just random operational noise.

### Adi

Adi is SVP Engineering and has given important context and support.

Key points from Adi:

- Bringing Routing to a healthy state is very important.
- The pod has not historically had strong management.
- It has behaved more like a collection of individuals than a durable team.
- There is a hero culture, especially among longer-tenured Datavant engineers.
- The goal is to move from “Vince owns this” to “Routing owns this.”
- Routing is one of the most critical points of failure in the organization.
- Routing may be one of the biggest leverage points for the business.
- The area needs clearer capacity thinking and explicit prioritization.
- Engineering leaders need more maturity in how they discuss these problems.
- Adi asked for a 3-week observation/readout to him, Neha and potentially other leaders.
- He sees Ryan as strong in context but possibly needing help with leadership gaps.
- He believes you may be able to help fill some of those gaps.

Working implication:

> Senior leadership sees the same core risks you are seeing. The opportunity is to turn those observations into a clear stabilization and scaling plan without making it a blame memo.

---

## 3. Core Problems Identified

### 3.1 Knowledge Concentration Around Vince

The biggest systemic people/process risk is that too much knowledge collapses back to Vince.

Symptoms:

- Vince is the primary source of truth.
- Engineers learn from him when they can get time with him, but learning is opportunistic.
- Temporary ICs may increase Vince’s onboarding burden instead of reducing work.
- Product and leadership may think help has been offered, but the help did not have enough context to be effective.
- Vince’s frustration grows because he sees people acting without understanding the system.
- Team dependency then appears to justify keeping work with Vince.

Current conclusion:

> The team does not just need more people. It needs structured knowledge transfer, secondary ownership and a model where Vince’s expertise creates leverage rather than dependency.

### 3.2 Support Load and Manual Work

Support is consuming the team and preventing strategic work.

Observed support issues:

- Too many support requests.
- Reroutes and manual interventions repeatedly hit Engineering.
- Support requests can bypass clean intake.
- Engineers sometimes do the requested action without enough time to investigate root cause.
- PPI/PPPI processes exist, but intake and prioritization still need work.
- DLQs and queue issues create ongoing operational drag.
- Member Locator incidents often pull in Vince.

Current conclusion:

> Support cannot be treated as incidental. It must be bounded, prioritized and linked to root-cause/system hardening work.

### 3.3 Product Scope Decisions Created Engineering Burden

Some prior product and migration decisions appear to have deferred feature/system work by assuming humans could manually handle gaps.

Consequences:

- Manual work turned out harder than expected.
- Inventory management became difficult.
- Engineering became the escape hatch for missing product/system capabilities.
- Customers may now expect quick manual intervention instead of waiting for hardened fixes.

Current conclusion:

> The team needs to stop solving every customer issue through manual engineering support. Product and Engineering need to decide when to accept customer delay in order to fix the underlying system.

### 3.4 Weak Onboarding

The team has no reliable onboarding system for permanent or temporary engineers.

Missing onboarding pieces:

- Product overview.
- Record request lifecycle.
- Current-state workflow docs.
- Architecture diagrams.
- Async process documentation.
- Glossary of core terms.
- Zone/team map.
- Support guide.
- Runbooks.
- First-ticket path.
- Knowledge transfer sessions.

Current conclusion:

> Onboarding is not a side project. It is a critical mechanism for reducing concentration risk.

### 3.5 Capacity Is Not Explicit

The team struggles to explain what is above the line and below the line.

Observed issues:

- New incidents can appear and no one can clearly say what falls off.
- High-priority work enters the team without enough explicit tradeoff.
- Support work consumes capacity but is not always fully represented in planning.
- Borrowed capacity may be counted optimistically even when it does not create immediate effective capacity.

Current conclusion:

> The team needs a visible capacity model that shows what is committed, what is at risk and what gets displaced when new work enters.

### 3.6 Current Team Composition May Not Match Complexity

Routing owns work that may require a more senior-heavy team than it currently has.

Current team concerns:

- Routing is too critical and complex to rely on one Staff engineer plus P3s.
- P3s can grow into the work, but they need structure and time.
- Temporary ICs without context do not solve the immediate problem.
- The team likely needs more P4/senior-plus capability.
- Some internal transfers may help if they bring relevant zone context.
- An external P4 could help bring fresh eyes without internal baggage.

Current conclusion:

> The team needs to evaluate whether its composition matches the ambiguity, support load and business importance of Routing.

---

## 4. Onboarding Conversation and Current Result

### What Started the Conversation

You noticed that Routing has essentially no onboarding system. This is especially dangerous because the team has deep system complexity, weak documentation, constant support interruptions and a single major SME bottleneck.

### What Good Onboarding Should Include

From prior experience, effective onboarding has two sides.

Product onboarding should explain:

- What the team owns.
- What UIs and workflows exist.
- What customers or operations teams experience.
- What the major statuses and process flows mean.
- How work moves through the business.

Engineering onboarding should explain:

- High-level architecture.
- What services, repos, jobs and queues the team owns.
- What is deployed and how it connects.
- Major workflows and async processes.
- Feature documentation.
- Diagrams for important flows.
- Current-state behavior versus goal-state design.

Zone onboarding should explain:

- What teams exist in the area.
- Who the EMs and PMs are.
- What each team owns.
- Where Routing fits.
- Which projects cross pod boundaries.

### Meeting With Connor and Vince

A meeting with Connor and Vince identified the following needs:

- Better documentation of the lifecycle of a record request.
- Better product documentation, especially statuses and sequential flow.
- Architecture diagrams.
- A tiered glossary.
- Current-state versus goal-state separation.
- Legacy system knowledge transfer.
- High-level zone/team map.
- Regular knowledge transfer sessions.
- Recorded pairing sessions with Vince.

### Minimal Onboarding v1

The minimal starting version should include:

1. Routing Team Onboarding Checklist
2. Routing Product Overview
3. Routing Current-State System Overview
4. Record Request Lifecycle
5. Routing Glossary
6. Routing Zone Map
7. Routing Support Guide
8. First 30 Days Plan

### Current Result

The team is starting to create an onboarding document. The first version is being treated as a framework of sessions and artifacts. The idea is not to build perfect documentation upfront, but to start with the minimum that helps engineers onboard and then improve it through recorded sessions, pairing and real onboarding use.

Current onboarding principle:

> Build onboarding around required context, not a giant documentation project.

---

## 5. 10/1 Deadline Conversation and Current Result

### Context

There is a 10/1 deadline involving several projects. The two projects discussed in detail were:

- Reroutes
- PEND code reassignment

### PEND Code Reassignment Concerns

Observed concerns:

- The project felt earlier-stage than the deadline suggested.
- The team still had many open questions.
- There was no clear tech spec.
- The EM was asking the PM questions that seemed like they should have been clarified before the meeting.
- Multiple dependent teams also lacked PRDs.
- Teams discussed creating sub-PRDs, which suggested decomposition was still immature.
- A borrowed engineer was expected to work on the project, but the work did not appear ready for execution.

Working framing:

> PEND code reassignment may not be in a controlled execution state. It needs clear requirements, technical scope, dependent-team ownership and executable tickets before it can be treated as on track.

### Reroutes Concerns

Initial understanding:

- Vince was building person-in-the-loop tooling.
- Once that worked, the team would remove the person from the loop.
- Andrew would then build the API/self-service capability around that foundation.

New concern:

- Vince later said the team may not have what it needs to remove the person from the loop.
- Vince estimated much of Andrew’s reroute work was blocked by the work he was doing.
- The reroute scripts were not doing what they needed to do.
- The team was at risk of putting UI/self-service on top of unreliable scripts.

Result this week:

- You got the right people into a room.
- The team recognized that the underlying scripts were not reliable enough.
- The work pivoted away from UI/self-service for now.
- The new focus is fixing the scripts and creating runbooks/documentation so the process still takes less engineering time.

Current conclusion:

> The reroute pivot was an early leadership win. It moved the team from automating an unreliable process toward hardening the foundation first.

### 10/1 Risk Framing

The right framing for leadership is:

> I do not want us to confuse activity with execution. People are busy, but I am not yet seeing the clarity I would expect if we were confidently marching toward 10/1.

Key risks:

- PEND still has open requirements and dependent-team questions.
- Reroutes depended on assumptions that changed.
- Support continues to consume capacity.
- Vince remains a bottleneck.
- Borrowed engineers may not add near-term capacity without context.

Current recommended action:

> Run a 10/1 execution reset. For each project, define the required outcome, current assumptions, open questions, dependencies, owner, earliest next action and green/yellow/red status.

---

## 6. Zone Structure and Restructure Conversation

### Context

Ryan has been considering changes to the zone and team structure. Sophie may move from EM back to IC, which creates a possible opening for a short-term restructure.

### Current Thinking

There may be two horizons:

1. **2026 stabilization change**
2. **2027 deliberate zone-design work**

For 2026, the idea is to use Sophie’s potential move as a catalyst to review engineers across teams and decide who best fits Routing’s immediate needs.

For 2027, the goal would be to intentionally evaluate:

- What the zone owns.
- Where system seams exist.
- What skills are needed.
- Which team boundaries make sense.
- Which teams should own which systems and workflows.
- How to build for the next 18–24 months.

### Team Composition Hypothesis

Routing may need to be more senior-heavy than the normal team shape.

Potential shape:

- Vince as Staff, but no longer sole owner.
- Two strong P4/senior-plus engineers.
- Kevin on an explicit P4 path.
- Magaly given structured ownership if the role fit is right.
- One internal transfer with relevant zone knowledge.
- One external P4 to bring fresh eyes.
- Clearer support boundaries.

### Charles

You would like to bring Charles in as a P4 if he is interested and fits the role. The value would be both senior capability and fresh perspective from someone not carrying Datavant baggage.

### Current Result

The restructure idea is not fully formed yet, but the direction is:

> Near-term, adjust team composition to stabilize Routing. Longer term, deliberately redesign the zone around ownership, system seams and future business needs.

---

## 7. Vince / Staff Engineer Expectations Conversation

### Why This Came Up

You are questioning whether Vince is operating at the Staff level in practice, or whether he may have been given Staff because of tenure and unique historical knowledge.

You are not questioning his technical strength. You are questioning whether his impact is multiplying the team.

### Relevant IC Ladder Context

The IC ladder says:

- Organizational impact is part of everyone’s role.
- Engineers are expected to accelerate the team.
- Organizational and cultural contributions are not distractions.
- Examples include knowledge transfer, documenting workflows, mentoring, pair programming and continuous improvement.
- P4s often mentor and uplevel junior engineers.
- P5 Staff Engineers are expected to have scope/complexity beyond P4, often across multiple pods or a whole vertical.
- A P5 is a go-to person for system knowledge, design decisions, team interfaces and improvement ideas.

### Current Concern

Vince meets much of the deep SME and go-to-person expectation, but may not be meeting the team-acceleration expectation strongly enough.

Potential language:

> Vince clearly has Staff-level system knowledge and technical judgment. The concern is whether his current operating model is creating Staff-level leverage or keeping the team dependent on him.

### Current Result

This is not yet something to escalate as “Vince is not Staff.” The safer and more useful frame is:

> Vince needs coaching to convert his knowledge into team leverage. That means more structured pairing, runbooks, decision logs, current-state docs and secondary owners.

---

## 8. Product / Support Tradeoff Conversation

### What Abby Clarified

Abby admitted that prior decisions skipped building features or parity because the belief was that manual handling could cover the gaps.

What happened:

- Manual handling was harder than expected.
- Inventory management became difficult.
- Engineering absorbed the work.
- Support load increased.
- Routing became the manual intervention point.

### Current Interpretation

This is a self-inflicted wound from scope reduction and migration tradeoffs.

Working framing:

> Some prior scope decisions converted missing product capability into recurring engineering support. Better support triage alone will not fix that. The team needs to harden the system and close the product gaps that keep generating support.

### Customer Tradeoff

The organization may need to accept that some customers wait for real fixes instead of getting immediate manual engineering intervention every time.

Better model:

- Triage impact.
- Decide when manual intervention is justified.
- Batch or defer lower-risk support asks.
- Fix root cause.
- Reduce future support.

Current conclusion:

> Product needs to own part of the pain created by deferred features. Engineering should not silently absorb every gap as manual support.

---

## 9. Emerging Memo / Leadership Readout

### Why a Memo Is Needed

Adi asked for a 3-week observation/readout. The memo should describe what you are seeing, where the risks are and how you plan to stabilize the pod.

This should not be a doom memo or a blame memo.

Working title:

> Routing Pod Stabilization and Scaling Plan

### Core Message

> Routing is a critical business capability with strong people, but it has been operating with too much knowledge concentration, reactive support load and unclear capacity. The path forward is to move from individual heroics to team ownership by improving intake, clarifying priorities, distributing system knowledge, tightening support boundaries and adjusting team composition around senior ownership.

### Likely Sections

1. What I observed
2. Why it matters to the business
3. Current risks
4. What is already improving
5. Team structure recommendation
6. Knowledge distribution and onboarding plan
7. Support and intake model
8. 30/60/90-day stabilization plan
9. Leadership asks

### Current Result

The memo should be built over the next two weeks and should become the artifact that aligns Ryan, Adi, Neha and other leaders around what Routing needs.

---

## 10. Current Working Plan

### Immediate Priorities

1. Continue onboarding and system ramp.
2. Finish getting local development environment fully working.
3. Continue building the Routing onboarding plan.
4. Help clarify 10/1 execution risks.
5. Support the reroute pivot toward script hardening and runbooks.
6. Start shaping the 3-week leadership readout.
7. Work with Ryan on capacity, team composition and potential restructure.
8. Coach Vince toward structured leverage rather than ad hoc heroics.
9. Build explicit development path for Kevin.
10. Give Magaly clearer scoped ownership and acceptance criteria.

### Near-Term Stabilization Goals

By end of 2026, show visible progress on:

- Reduced Vince dependency.
- Better onboarding artifacts.
- Clearer support intake.
- More explicit capacity planning.
- Better Product/Engineering tradeoffs.
- A credible team composition plan.
- Stronger senior ownership around Routing systems.

### Longer-Term Goals

For 2027:

- Deliberate zone design.
- Clear system ownership boundaries.
- More durable team structure.
- Reduced hero culture.
- Stronger engineering operating model.
- Better observability and monitoring for core Routing/Switchboard workflows.
- A team where Routing owns Routing, not Vince.

---

## 11. Working Principles Going Forward

### Do Not Frame This as a People Failure

The team has strong people, but the system has made the wrong behaviors rational.

Better framing:

> The team is operating in a model that overuses heroics, hides capacity, concentrates knowledge and converts product gaps into engineering support.

### Distinguish Capacity From Effective Capacity

A strong engineer without context may become capacity later, but may create more load in the short term.

Better framing:

> The question is not just how many engineers are assigned. The question is how much effective Routing capacity exists after accounting for context, support load, onboarding cost and system complexity.

### Fix Foundations Before Automating Them

Do not put UI, self-service or automation on top of unreliable scripts or unclear workflows.

Better framing:

> Automation should reduce risk, not scale broken behavior.

### Move From Vince Owns This to Routing Owns This

This is the central cultural and operating shift.

Better framing:

> Vince’s knowledge should become a team asset, not a team dependency.

### Make Tradeoffs Explicit

When new work enters, something else must move.

Better framing:

> If an incident or support request moves above the line, we need to know what moves below the line.

### Treat Onboarding as Risk Reduction

Onboarding is not administrative overhead. It is the mechanism for reducing key-person risk.

Better framing:

> Every onboarding artifact should reduce future dependency on a single person.

---

## 12. Useful Phrases for Future Conversations

### On Routing’s Problem

> I think Routing’s issue is less about raw capacity and more about effective capacity. The system is complex, the context is concentrated and support load keeps pulling people away from the work that would make the team healthier.

### On Vince

> Vince clearly has Staff-level system knowledge and technical judgment. The question is whether his current operating model is creating Staff-level leverage or reinforcing the dependency we are trying to break.

### On Temporary Help

> A strong engineer without Routing context may help eventually, but if we count them as capacity too early, we may accidentally increase Vince’s load instead of reducing it.

### On Support

> Some prior scope decisions appear to have converted missing product capability into recurring engineering support. Better triage helps, but we also need to close the gaps that keep generating the support.

### On Product Tradeoffs

> Product and Engineering need to jointly decide when manual intervention is worth it and when we should let the pain surface long enough to fix the root cause.

### On Reroutes

> The reroute reset was important because automating an unreliable workflow would have moved the risk around instead of reducing it.

### On Structure

> I think we should separate near-term stabilization from longer-term zone design. For 2026, we should make the minimum structural changes needed to stabilize Routing. For 2027, we should deliberately evaluate the zone seams, ownership model and team boundaries.

### On Leadership Memo

> This should not be a blame memo. It should be a stabilization plan for a critical business capability.

---

## 13. Context Intentionally Excluded

This file intentionally does not include:

- Interview process details.
- Offer details.
- Compensation.
- Benefits.
- Payroll.
- RSUs.
- Job-search history.
- Resume strategy.
- Other companies or opportunities.

