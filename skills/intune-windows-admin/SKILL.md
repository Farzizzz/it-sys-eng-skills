---
name: intune-windows-admin
description: Use for Microsoft Intune administration of Windows endpoints only - compliance policies, configuration profiles, Windows Autopilot, app deployment, and how Intune compliance feeds Conditional Access. Invoke for "Intune", "Windows compliance policy", "Autopilot", "configuration profile", or "Conditional Access" in a Windows context.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: endpoint-management
  triggers: Intune, Windows, compliance policy, configuration profile, Autopilot, Conditional Access, Endpoint Manager, MEM
  role: specialist
  scope: administration
  output-format: config
  related-skills: mac-mdm-admin, okta-admin, security-reviewer
---

# Intune Administrator (Windows)

Microsoft Intune administration for Windows endpoints in Corp IT / TechOps.

## Hard rule: Windows only

Intune manages **Windows** endpoints. macOS is managed by the Mac MDM (Kandji) - see `mac-mdm-admin`. Never reach for Intune in a Mac context, and never assume a device is Windows: if the platform is not stated, ask which it is, because the answer changes entirely.

## Core workflow

1. Confirm the platform is Windows and identify the device or group.
2. Make the change (compliance policy, configuration profile, or app assignment), assigned to a group rather than per device.
3. Sync the device (or wait for the check-in cycle) and refresh the report.
4. Verify the result in the device view, and confirm any Conditional Access impact.

## Compliance policies

- Assign compliance policies to the device/user group, not individually.
- Windows devices check in on a cycle (roughly every 8 hours); after a change, use Sync to force it sooner, then refresh the report rather than trusting the stale view.
- Watch for expected false negatives: a rule that does not apply to a given Windows build or form factor can report Not compliant for a benign reason. Confirm the cause before treating it as a real failure.

## Configuration profiles and Autopilot

- Group assignments again, and read the per-profile status (Succeeded / Error / Not applicable). "Not applicable" is often expected; "Error" is a real failure to investigate.
- Autopilot device preparation runs on first sign-in and can take around 10 minutes and reboot. The user must wait and must not close the setup window, or enrolment can break and need a rebuild.

## Conditional Access interaction

- Intune compliance feeds Conditional Access: a "require compliant device" grant will block a device Intune reports as non-compliant. Before enforcing broadly, confirm the compliance policies are clean for the target population so you do not lock users out.

## Guardrails

- Never apply a change without knowing it is a Windows device.
- Flag any change that could trip Conditional Access and lock users out before you make it.
- Do not invent CSP names or policy settings. If unsure, say so and check the current Microsoft Intune docs.
