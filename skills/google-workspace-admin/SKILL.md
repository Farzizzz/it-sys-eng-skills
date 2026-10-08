---
name: google-workspace-admin
description: Use for Google Workspace administration - users, groups, organisational units (OUs), shared drives, and GAM / GAMADV automation. Invoke for "Google Workspace", "GAM", "OU", "shared drive", "Workspace group", "suspend user", or bulk Workspace changes.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: collaboration
  triggers: Google Workspace, GAM, GAMADV, organisational unit, OU, shared drive, Workspace group, suspend user, Gmail admin, Drive admin
  role: specialist
  scope: administration
  output-format: script
  related-skills: identity-lifecycle-jml, okta-admin, security-reviewer
---

# Google Workspace Administrator

Google Workspace administration for Corp IT / TechOps, including GAM / GAMADV automation.

## Corp IT / TechOps context

- Common tasks: user lifecycle, group membership, OU moves, shared drive membership and permissions, and reporting pulls.
- Prefer a scripted, repeatable GAM command with evidence over a one-off console change when the task is bulk or needs an audit trail.

## GAM safety (read before any bulk or destructive command)

GAM runs with admin authority and can change or delete a lot very quickly (bulk delete or suspend, OU moves, Drive ACL changes, group membership wipes). Treat it as high blast radius.

- Always warn and get explicit confirmation before running any destructive or bulk GAM command.
- Print or dry-run first: run the read/`print` form, confirm the target set is exactly what you expect, then run the change.
- Prefer suspend over delete for offboarding unless deletion is explicitly required.
- Scope bulk operations from a reviewed input list, not an open-ended query, and keep the command and its output as evidence.

## Core workflow

1. Define the exact target set (one user, a group, or a reviewed CSV) and the intended end state.
2. Run the read / `print` form first and confirm the set.
3. Get explicit confirmation for anything destructive or bulk.
4. Run the change, capture the output.
5. Verify in the Admin console or via a follow-up `print`.

## Scripts

Any GAM wrapper or Apps Script you produce carries a header comment with `Script Author: Farz Owasil`, a one-line purpose, prerequisites (scopes, admin, token), and the date last updated.

## Guardrails

- No destructive or bulk GAM command without explicit confirmation and a prior print/dry-run.
- Suspend, do not delete, unless deletion is explicitly asked for.
- Do not invent GAM command syntax or arguments. If unsure, say so and check the current GAM / GAMADV docs.
