# Documentation Standards Proposal

## Purpose

The goal of this proposal is to make documentation **predictable and discoverable**. Someone looking for information should not need to know who created it, remember an old Slack thread, or already know where it lives.

We will use four primary locations based on the documentation's **audience and purpose**.

| Location | Use For | Examples |
| ----- | ----- | ----- |
| **Repository** | Documentation specific to engineers working with the code | README files, setup/build/test instructions, configuration, implementation details, repo-specific troubleshooting |
| **Google Docs** | Documents where collaboration, comments, review, and iteration are important | PRDs, RFCs, design proposals, project plans, discovery docs, drafts |
| **Confluence** | Durable Product & Engineering knowledge and discovery | Team information, architecture, workflows, working agreements, runbooks, project pages, onboarding |
| **Loop** | Finalized, polished documentation for broad Datavant consumption | CS/Operations workflows, troubleshooting guides, support procedures, finalized plans, cross-functional guidance |

These are **not stages that every document moves through**. A document can remain permanently in any of these locations when that is its appropriate home.

## Repository Documentation

Documentation tightly coupled to a codebase should live with the code and evolve with it.

A README or other repository documentation does **not** need to be migrated into Google Docs or Confluence when it becomes mature. It should remain in the repository when that is its natural home.

Repository documentation can link to Google Docs or Confluence, and those systems can link back to repository documentation.

## Google Docs

Google Docs should be the default when active collaboration is important.

A Google Doc does not need to move somewhere else when collaboration ends. It can remain the authoritative document permanently.

When a Google Doc contains durable information, it should be made discoverable through the appropriate Confluence project, team, or system page.

## Confluence

Confluence is the primary home and **discovery layer** for durable Product & Engineering knowledge.

Not everything needs to be copied into Confluence. A Confluence page can point to authoritative Google Docs, repository documentation, Lucid diagrams, or other resources.

However, links need context. Someone finding the Confluence page through search should understand what the linked resource contains and why it is relevant.

For example, instead of:

> **PRD:** \[link\]

Prefer:

> **Product Requirements Document:** Final PRD covering project requirements, scope decisions, user workflows, and acceptance criteria. \[link\]

At a minimum, teams should maintain a Confluence presence that describes:

* **Who we are** – EM, PM, engineers, and other regular team members  
* **What we own** – Products, services, systems, and team responsibilities  
* **How we work** – Important workflows, working agreements, support responsibilities, and escalation paths  
* **Architecture** – Higher-level system documentation and links to relevant diagrams or technical resources

## Loop

Loop is the publishing destination for documentation intended for broad Datavant consumption.

Content published in Loop should be:

* Finalized and polished  
* Written for its intended organizational audience  
* Self-contained  
* Usable without access to Product & Engineering systems

**Loop should not depend on links to Confluence, Google Docs, repositories, or other Product & Engineering documentation.**

If information from those systems is needed by the broader audience, the relevant information should be incorporated into the Loop document itself.

Some duplication between Loop and Product & Engineering documentation is therefore intentional and acceptable. The audiences and purposes are different.

## Discoverability and Linking

Within Product & Engineering, documentation should link freely when it helps people find the authoritative information:

**Repositories ↔ Google Docs ↔ Confluence**

The important rule is that links should include enough context to be discoverable. Avoid pages that are simply collections of unexplained links.

Confluence should provide the primary discovery path for durable Product & Engineering knowledge, even when the authoritative document itself lives elsewhere.

Loop is the exception. Moving information into Loop should be treated as **publishing**, not linking:

**Product/Engineering knowledge → Self-contained Loop documentation**

## Ownership and Maintenance

Durable documentation should have an identifiable owning team.

As part of completing projects or making meaningful operational changes, teams should ask:

* Where is the authoritative documentation?  
* Can someone unfamiliar with the work discover it?  
* Does existing documentation need to be updated?  
* Are we creating competing sources of truth?  
* Is it clear which team owns keeping this information current?  
* If broader Datavant consumption is needed, do we need a self-contained Loop document?

The goal is not to document everything or enforce rigid tooling. The goal is to make it **clear where information belongs, easy to find later, and clear who is responsible for keeping it useful.**

