---
name: incident-response-it
description: Use for IT incident management - severity classification, incident roles, impact-first status updates, timeline capture, and post-incident review. Triggers: incident, outage, major incident, incident commander, status update, post-incident review, postmortem.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: reliability
  triggers: incident, outage, major incident, incident commander, status update, post-incident review, postmortem
  role: specialist
  scope: process
  related-skills: sre-engineer, monitoring-expert
---

# IT Incident Response

Response and communications for IT service incidents in Corp IT / TechOps (access outages, mail, network, endpoint fleet). The reliability-engineering side lives in `sre-engineer`.

## Severity

Classify by impact and scope: how many users, which service, and whether there is a workaround. Agree the severity before arguing about cause, because it sets the comms cadence and who gets pulled in.

## Roles

- Incident commander: owns the response and the decisions, not the hands-on fix.
- Scribe: captures the timeline (times, actions, decisions).
- Comms: sends updates to stakeholders.

On a small incident one person may hold several roles, but name them so nothing is dropped.

## Communications (impact-first)

Lead with impact and current status, then cause if known, then the next update time. Keep each update short and factual. Example:

Impact: staff in the London office cannot sign in to email. Status: identified, fix in progress. Cause: a Conditional Access change this morning. Next update: 14:30, or sooner if it clears.

## Workflow

1. Declare the incident and set severity.
2. Assign roles.
3. Send the first stakeholder update quickly (impact, status, next update time), even before the cause is known.
4. Keep a running timeline.
5. Resolve, confirm with affected users, then close.
6. Run a blameless post-incident review: timeline, impact, what happened, contributing factors, and follow-up actions with owners.

## Guardrails

- Impact and status before cause in every update, and always give a next-update time and keep it.
- The post-incident review is blameless and focuses on systemic fixes, not individuals.
- Do not state a cause as certain until it is confirmed: say what is known and what is still being investigated.
