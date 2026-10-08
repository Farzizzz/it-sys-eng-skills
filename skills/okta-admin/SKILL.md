---
name: okta-admin
description: Use for Okta identity and access administration - group rules, application assignments, SSO (SAML/OIDC) and SCIM provisioning, user lifecycle, and changes made via the Okta API or the Terraform okta provider. Invoke for "Okta group rule", "app assignment", "SCIM", "SAML app", "Okta API", "user lifecycle", or "deprovision in Okta".
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: identity
  triggers: Okta, IAM, group rule, app assignment, SAML, OIDC, SCIM, provisioning, lifecycle, okta terraform provider
  role: specialist
  scope: administration
  output-format: config
  related-skills: identity-lifecycle-jml, security-reviewer, google-workspace-admin
---

# Okta Administrator

Okta IAM administration for Corp IT / TechOps. Okta is the identity source of truth, so changes here are high blast radius and reviewed carefully before they go wide.

## Corp IT / TechOps context

- Prefer a reviewed, repeatable change path (the Terraform okta provider, or a scripted API call) over ad hoc console edits whenever the change is repeatable or needs an audit trail.
- Test every group rule or assignment change on a single user before rolling it out broadly.

## Core workflow

1. Scope the change: who is in scope, which apps or groups, and what "done" looks like.
2. Check attribute reliability before matching on it (see the gotcha below).
3. Make the change via the chosen path (Terraform, API, or console) and keep the evidence.
4. Verify: assigned apps, the Okta System Log entry for the change, and a test sign-in.
5. Record who changed what and when.

## Group rules and assignments

- Gotcha: a group rule that matches on a sparsely populated attribute (for example `user.department`) will silently drop users in offices or regions where that attribute is not populated. Confirm the attribute is populated for every intended user, or match on a reliably populated attribute, or backfill the attribute first.
- Roll out to one test user, confirm the expected app assignment, then widen.

## SSO (SAML / OIDC) and SCIM

- For a new app, decide SAML vs OIDC, configure the ACS/redirect values from the vendor, and assign via group rather than per user.
- Where the app supports SCIM, enable provisioning and map only the attributes you need. Confirm create, update, and deactivate all behave before relying on it for lifecycle.

## Lifecycle and deprovision

- Suspend vs deactivate: suspend is reversible and keeps assignments, deactivate tears down downstream SCIM provisioning. Pick deliberately.
- Treat deactivate and delete as destructive. Confirm the user and the intent before running, and capture the System Log evidence.

## Guardrails

- Never push a broad group-rule or app-assignment change without a single-user test and confirmed attribute coverage.
- Deactivation and deletion are destructive: confirm first.
- Do not invent Okta Expression Language functions or API fields. If unsure of exact syntax, say so and check the current Okta developer docs.
