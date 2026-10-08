---
name: identity-lifecycle-jml
description: Use for Joiner / Mover / Leaver (JML) identity lifecycle across Okta and Google Workspace. Invoke for onboarding a starter, role or department moves, offboarding a leaver, and suspend vs deactivate vs delete decisions. Triggers: JML, joiner, mover, leaver, onboarding, offboarding, deprovision, suspend user, identity lifecycle.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: identity
  triggers: JML, joiner, mover, leaver, onboarding, offboarding, deprovision, suspend, deactivate, lifecycle
  role: specialist
  scope: process
  related-skills: okta-admin, google-workspace-admin, security-reviewer
---

# Identity Lifecycle (Joiner / Mover / Leaver)

Joiner / Mover / Leaver orchestration across Okta (IAM) and Google Workspace for Corp IT / TechOps, triggered by an HR event. Sequencing and reversibility matter more than speed.

## Corp IT / TechOps context

- The HR joiner/leaver feed is the trigger of record. Okta is the IAM source of truth and Google Workspace is the primary collaboration account.
- Prefer reversible actions first and keep evidence of every lifecycle change.

## Joiner

1. Validate the person against the HR record before creating anything, to avoid typos and duplicates.
2. Create and activate the Okta user, assigning apps and groups by rule rather than by hand (see `okta-admin` and the attribute-coverage trap).
3. Provision the Google Workspace account and the right group / OU membership.
4. Confirm first sign-in and MFA enrolment.

## Mover (role or department change)

1. Update the authoritative attributes, specifically the ones group rules match on.
2. Re-evaluate rule-driven assignments: a move is a grant and a revoke, not just a grant.
3. Confirm the access that should drop has actually dropped.

## Leaver (offboarding): order and reversibility

Okta lifecycle states are `STAGED, PROVISIONED, ACTIVE, RECOVERY, LOCKED_OUT, PASSWORD_EXPIRED, SUSPENDED, DEPROVISIONED`. In the Admin Console, "Deactivated" is the API state `DEPROVISIONED`.

1. Suspend first. Okta `SUSPENDED` retains app assignments and blocks Okta access, and it is reversible (unsuspend returns the user to `ACTIVE`). This is the safe immediate step when someone leaves.
2. Suspend the Google Workspace account too: reversible, data retained, still billed. Do not delete yet.
3. Deactivate or delete only per the retention policy and after any data handover:
   - Okta deactivate (`DEPROVISIONED`) removes all app assignments and deletes the password, which is destructive. Re-activation is only possible from `STAGED` or `DEPROVISIONED`.
   - Workspace delete: a deleted user is restorable for about 20 days, then permanent, and restore needs an available licence. Transfer Drive and mail before deleting.

## Guardrails

- Suspend before you deactivate or delete. Never delete an active user just to free a licence.
- A mover is a revoke as well as a grant: check that dropped access actually dropped.
- Validate the person against HR before any create or destructive step.
- Do not invent Okta states or Workspace retention numbers. Verify against the Okta user-lifecycle docs and Google Workspace Admin Help.
