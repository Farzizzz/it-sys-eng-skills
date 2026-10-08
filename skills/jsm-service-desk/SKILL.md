---
name: jsm-service-desk
description: Use for Jira Service Management administration - request types, queues (built with JQL), SLAs, and automation. Invoke for setting up a service desk, triaging queues, configuring SLA goals, or writing JSM automation. Triggers: Jira Service Management, JSM, service desk, request type, queue, SLA, automation, JQL queue.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: service-management
  triggers: Jira Service Management, JSM, service desk, request type, queue, SLA, automation, JQL
  role: specialist
  scope: administration
  related-skills: atlassian-mcp
---

# Jira Service Management (service desk)

Jira Service Management administration for Corp IT / TechOps. For general Jira and Confluence work (JQL, CQL, tickets), see `atlassian-mcp`.

## Corp IT / TechOps context

- JSM runs the IT service desk: intake through request types, triage through queues, time goals through SLAs, and repetitive work through automation.

## Core concepts (verified terms)

- Request types: the kinds of requests customers raise, organised into portal groups.
- Queues: lists of incoming requests for agents to triage. Queues are built with JQL via the advanced editor (a basic editor also exists), and JQL is also used for SLAs.
- SLAs: time-based goals with calendars and start, pause, and stop conditions.
- Automation: rules that act on a trigger and conditions. Atlassian's wording varies by version (automation rules, flows, Legacy automation), so confirm the term in your instance rather than assuming one.

## Core workflow

1. Define request types and map them to portal groups.
2. Build agent queues with JQL (advanced editor) so triage matches your process.
3. Set SLA goals with the correct calendar and start/pause/stop conditions.
4. Add automation for repetitive actions (assignment, transitions, notifications), and test on a sample issue first.

## Guardrails

- JSM UI and terminology shift between versions: confirm exact labels and the automation wording against current Atlassian docs.
- Validate JQL on a small result set before saving a queue or an SLA.
- Do not invent JQL fields or automation components. Verify against the Atlassian support docs.
