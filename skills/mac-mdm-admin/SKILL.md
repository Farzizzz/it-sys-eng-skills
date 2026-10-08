---
name: mac-mdm-admin
description: Use for macOS endpoint management via Kandji - Blueprints, Library Items, compliance, Automated Device Enrolment (ADE), and app deployment. Invoke for "Mac MDM", "Kandji", "macOS compliance", "Blueprint", "Library Item", or "Mac enrolment".
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: endpoint-management
  triggers: Kandji, macOS, Mac MDM, Blueprint, Library Item, ADE, Automated Device Enrolment, Mac compliance, Mac enrolment
  role: specialist
  scope: administration
  output-format: config
  related-skills: intune-windows-admin, okta-admin, security-reviewer
---

# Mac MDM Administrator (Kandji)

macOS endpoint management via Kandji for Corp IT / TechOps.

## Hard rule: macOS only

Kandji manages **macOS** endpoints. Windows is managed by Intune - see `intune-windows-admin`. Never apply a Mac answer to a Windows device or vice versa, and if the platform is not stated, ask which it is before answering, because the tool and the steps change entirely.

## Core workflow

1. Confirm the device is a Mac and identify the device or the Blueprint it belongs to.
2. Make the change as a Library Item assigned to the right Blueprint, rather than a one-off on a single device.
3. Let the device check in (or trigger it), then confirm the Library Item status.
4. Verify compliance and that any dependent access still works.

## Blueprints and Library Items

- Blueprints are the assignment unit: a device gets its configuration, apps, and compliance from the Blueprint it is assigned to. Make the change at the Blueprint / Library Item level so it is repeatable, not per device.
- Test a changed Library Item on one device in the Blueprint before relying on it fleet-wide.

## Enrolment (ADE)

- Automated Device Enrolment binds a Mac to the MDM at setup via the reseller / Apple Business Manager feed. Confirm the device shows in the ADE list and lands in the intended Blueprint.
- A device that enrols into the wrong Blueprint gets the wrong configuration silently: check the assignment after enrolment.

## Compliance

- Read the Library Item and compliance status per device, and force a check-in after a change rather than trusting a stale view.
- Distinguish a genuine failure from an item that is simply not yet applied or not applicable to that macOS version.

## Guardrails

- Never apply a change without confirming it is a Mac.
- Treat device actions that wipe or lock (erase, remote lock) as destructive: confirm the device and intent first.
- Do not invent Kandji Library Item names or API fields. If unsure, say so and check the current Kandji docs.
