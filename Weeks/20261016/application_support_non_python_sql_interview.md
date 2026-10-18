# Enterprise Application Support Engineer
## Troubleshooting & Support Interview Question Bank

### Interview Goal

Evaluate whether the candidate can take an ambiguous support problem, investigate it independently, work effectively across teams, and create a high-quality escalation when Engineering involvement is needed.

The goal is not to find a heads-down software engineer. We are looking for someone who:

- Is good at working with people.
- Knows where to look when a problem is reported.
- Is comfortable digging into unfamiliar issues.
- Can assist with technical troubleshooting.
- Can distinguish between bugs, feature requests, configuration issues, and operational issues.
- Understands enough about Engineering, Product, and Operations to work effectively across those groups.
- Can review code and technical artifacts even when they are not the author.
- Documents what they investigated and what they found.
- Escalates appropriately instead of immediately handing problems to Engineering.
- Is willing and able to learn areas where they do not already have deep expertise.

---

## 1. Ambiguous Problem / Troubleshooting Approach

### Question

A customer reports:

> "Our integration stopped working."

That is all the information you have initially.

Walk me through what you would do.

### What to Look For

The candidate should begin narrowing the problem rather than guessing at a cause.

Good signals include:

- Clarifying expected vs. actual behavior.
- Establishing when the problem started.
- Determining scope and customer impact.
- Asking whether anything changed recently.
- Gathering concrete examples, IDs, timestamps, requests, or affected records.
- Looking at logs, metrics, configuration, or data.
- Attempting to reproduce the issue.
- Tracing the problem through relevant systems.
- Forming and testing hypotheses.
- Documenting what they find.

### Follow-up Prompts

- What would you want from the person reporting the issue?
- What would you investigate yourself before escalating?
- How would you determine whether this is a bug, configuration problem, or something else?
- When would you involve another team?

---

## 2. Microservices / Queue Throughput Scenario

### Scenario

A service normally processes around **1,000 records per minute**.

Today it is processing around **200 records per minute**.

There are multiple services involved, and records move through queues between them. You do not know where the slowdown is.

### Question

Walk me through how you would investigate this.

### What to Look For

There is not one required answer. Look for whether the candidate can build a mental model of the system and systematically narrow down where the problem exists.

Strong signals include investigating:

- Whether incoming volume has changed.
- Whether a queue backlog is growing.
- Which queue or service appears to be the bottleneck.
- Consumer throughput.
- Error and retry rates.
- Recent deployments or configuration changes.
- CPU, memory, or other resource constraints.
- Database performance or latency.
- Downstream service/API latency.
- Instance health.
- Concurrency or worker counts.
- Whether particular records are repeatedly failing or taking longer.
- Logs, metrics, and traces.
- Differences between a normal period and the degraded period.

The important behavior is identifying **where data stops moving at the expected rate**.

### Follow-up

You discover that the incoming queue is growing rapidly, but the consumer is not reporting errors.

What would you investigate next?

### Additional Follow-up

At what point would you escalate this to Engineering?

What information would you include in the escalation?

---

## 3. Support-to-Engineering Escalation

### Question

You have spent time investigating a production issue and now believe it may be a software defect.

What would you send Engineering?

### What to Look For

A strong escalation should contain enough information for Engineering to begin investigating without repeating all of Support's work.

Look for:

- Customer/business impact.
- Severity and scope.
- Expected behavior.
- Actual behavior.
- Reproduction steps, when available.
- Example record IDs, request IDs, correlation IDs, or timestamps.
- Relevant logs or errors.
- Data gathered during investigation.
- Things already attempted.
- Results of those attempts.
- Relevant environment/configuration information.
- Current hypothesis.
- Clear statement of what help is needed from Engineering.

### Follow-up

Engineering responds:

> "Can't reproduce."

What do you do next?

### What to Look For

The candidate should continue owning the investigation rather than treating the escalation as a handoff.

---

## 4. Knowing When to Escalate

### Question

How do you decide when you have investigated enough and should escalate an issue?

### What to Look For

Good candidates balance independence with knowing when continuing alone is wasting time or increasing risk.

Listen for consideration of:

- Customer impact.
- Severity.
- Time sensitivity.
- SLA expectations.
- Access or permission boundaries.
- Whether code changes are required.
- Whether they have exhausted reasonable troubleshooting paths.
- Whether specialist knowledge is needed.
- Risk of taking further action themselves.

Avoid candidates whose default answer is either:

- Escalate immediately.
- Never escalate until they personally solve the problem.

---

## 5. Runbook Judgment

### Scenario

You are following a production runbook.

At step 6, the system produces a result different from what the runbook says you should see.

### Question

What do you do?

### What to Look For

Strong candidates should not blindly continue executing instructions.

Good signals include:

- Stop and understand the unexpected state.
- Verify previous steps.
- Confirm inputs and environment.
- Review logs or system state.
- Consider whether the runbook is outdated.
- Understand the risk before continuing.
- Ask for help when appropriate.
- Document the discrepancy.
- Improve or flag the runbook afterward.

---

## 6. Bug vs. Feature Request

### Scenario

A customer says:

> "The application should automatically retry this operation when it fails. It doesn't, so this is a bug."

You do not know whether automatic retry is expected behavior.

### Question

How would you determine whether this is a defect, feature request, configuration issue, or expected behavior?

### What to Look For

Look for whether the candidate gathers evidence before categorizing the issue.

Possible investigation:

- Understand the customer's expected workflow.
- Reproduce the behavior.
- Check documentation.
- Review configuration.
- Compare against requirements or acceptance criteria.
- Look for existing issues or known limitations.
- Consult Product or Engineering when necessary.
- Clearly explain the result back to the customer or internal stakeholder.

---

## 7. Working Across Teams

### Question

Tell me about a production issue where you had to work with multiple groups to resolve the problem.

### Follow-up Prompts

- What was your role?
- How did you determine who needed to be involved?
- How did you keep everyone aligned?
- Where did ownership sit?
- What did you personally investigate?
- How did you communicate the resolution?

### What to Look For

Look for candidates who can coordinate without simply becoming a message relay between teams.

---

## 8. Managing Expectations During an Incident

### Scenario

You are handling a high-priority production issue.

Engineering believes the fix may take several days, but the business or customer expects it to be resolved today.

### Question

How would you handle the situation?

### What to Look For

Good signals include:

- Clear communication about what is known and unknown.
- Avoiding promises they cannot make.
- Understanding business/customer impact.
- Looking for mitigations or workarounds.
- Establishing an update cadence.
- Keeping technical teams focused while maintaining stakeholder communication.
- Translating technical constraints into understandable language.

---

## 9. Prioritization

### Scenario

You have five open support cases.

Two customers say their issue is urgent.

### Question

How do you decide what to work on first?

### What to Look For

Listen for reasoning based on:

- Customer/business impact.
- Severity.
- Number of affected users or records.
- Production availability.
- Data loss or integrity risk.
- SLA.
- Availability of workarounds.
- Age of the issue.
- Dependencies on other teams.

"Who is complaining the loudest" should not be the primary prioritization mechanism.

---

## 10. Documentation

### Question

After resolving a difficult production issue, what do you document?

### What to Look For

Strong answers may include:

- Symptoms.
- Impact.
- Root cause, if known.
- Investigation performed.
- Useful queries or commands.
- Resolution or workaround.
- Validation performed.
- Follow-up actions.
- Runbook or knowledge-base improvements.
- Monitoring or alerting gaps.
- Recurrence prevention.

### Follow-up

How do you decide whether something belongs in a ticket, runbook, knowledge base, or engineering backlog?

---

## 11. Using AI in Support and Troubleshooting

### Question

How are you using AI tools in your work today?

Give me an example where AI helped you troubleshoot or understand something technical.

### Follow-up

How do you verify that what the AI gives you is correct?

### What to Look For

Useful applications might include:

- Understanding unfamiliar code.
- Interpreting errors.
- Generating or reviewing queries.
- Summarizing logs.
- Brainstorming troubleshooting hypotheses.
- Learning an unfamiliar technology.
- Drafting documentation.
- Explaining unfamiliar system behavior.

The strongest signal is not which AI tool they use. It is whether they treat AI output as something to **verify against actual code, data, documentation, logs, tests, or system behavior**.

### Potential Concerns

- Refuses to use AI categorically without a thoughtful reason.
- Treats AI output as authoritative without verification.
- Shares sensitive data without considering security/privacy implications.

---

# Overall Evaluation

Consider the candidate across these dimensions:

| Dimension | What We Are Evaluating |
|---|---|
| Troubleshooting | Can they systematically narrow an ambiguous problem? |
| Technical reasoning | Can they reason about applications, services, queues, data, APIs, and system behavior? |
| Resourcefulness | Do they investigate and use available tools before escalating? |
| Escalation judgment | Do they know when and how to involve Engineering? |
| Ownership | Do they continue driving an issue after other teams become involved? |
| Communication | Can they explain technical issues clearly to different audiences? |
| Documentation | Can they leave behind useful information for the next person? |
| Learning mindset | Can they work effectively in areas where they are not already an expert? |
| AI usage | Can they use AI productively while independently validating its output? |

## Overall Hiring Question

The goal is not to determine whether the candidate already knows every technology in the platform.

The broader question is:

> **Does this person have enough technical foundation, troubleshooting instinct, ownership, and learning ability that we can work with them on the things they do not already know?**
