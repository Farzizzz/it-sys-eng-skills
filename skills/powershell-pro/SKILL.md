---
name: powershell-pro
description: Use for PowerShell scripting for Windows and Microsoft 365 admin - the Microsoft Graph PowerShell SDK, Exchange Online, and Teams. Invoke for Connect-MgGraph, Graph scopes, or Exchange Online / Teams PowerShell. Triggers: PowerShell, Microsoft Graph, Connect-MgGraph, Exchange Online, Teams PowerShell, M365 admin.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: automation
  triggers: PowerShell, Microsoft Graph, Connect-MgGraph, Exchange Online, Teams PowerShell, M365 admin, Graph SDK
  role: specialist
  scope: implementation
  output-format: script
  related-skills: python-pro, intune-windows-admin, okta-admin
---

# PowerShell Pro (Windows and M365 admin)

PowerShell for Windows and Microsoft 365 administration in Corp IT / TechOps. Pair with `python-pro` for cross-platform work.

## Corp IT / TechOps context

- Any `.ps1` you produce carries a header comment with `Script Author: Farz Owasil`, a one-line purpose, prerequisites (modules, scopes, roles), and the date last updated.

## Modules and connecting (verified)

- Microsoft Graph PowerShell SDK ships as two modules: `Microsoft.Graph` (v1.0 endpoint) and `Microsoft.Graph.Beta` (beta). The core is `Microsoft.Graph.Authentication`. You choose v1.0 vs beta by which module and cmdlet you use, not a profile switch. Prefer v1.0 for scripts, as beta can change.
- Connect: `Connect-MgGraph -Scopes "User.Read.All","Group.ReadWrite.All"` (scopes are a string array). The cmdlet noun prefix is `Mg` (for example `Get-MgUser`); beta cmdlets use `MgBeta`.
- Exchange Online: module `ExchangeOnlineManagement`, with `Connect-ExchangeOnline` and `Disconnect-ExchangeOnline`. Security and Compliance uses `Connect-IPPSSession` from the same module.
- Teams: module `MicrosoftTeams`, with `Connect-MicrosoftTeams`.

## Core workflow

1. Install only the Graph sub-modules you need (the full `Microsoft.Graph` pulls in 40+). Discover commands and the permissions they need with `Find-MgGraphCommand`, and list modules with `Find-Module Microsoft.Graph*`.
2. Connect with least-privilege scopes.
3. Script defensively: `try/catch` with `-ErrorAction Stop`, accept pipeline input, and keep secrets out of the script (app-only certificate auth, or a secret pulled from a vault).
4. Disconnect when done.

## Gotchas (verified)

- Exchange Online: frequent `Connect-ExchangeOnline` / `Disconnect-ExchangeOnline` in one session can leak memory. Limit the cmdlets loaded with `-CommandName`, and disconnect so you do not exhaust available sessions.
- Do not hardcode module version numbers: check with `Get-InstalledModule` or the PowerShell Gallery. The old `Select-MgProfile` approach was replaced by the two-module (v1.0 / beta) model.

## Guardrails

- Least-privilege Graph scopes, and prefer app-only certificate auth for unattended scripts.
- Never invent cmdlet or parameter names. If unsure something exists, say so and check Microsoft Learn (Graph PowerShell, Exchange Online PowerShell, Teams PowerShell).
