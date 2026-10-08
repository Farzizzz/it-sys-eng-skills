---
name: apps-script-automation
description: Use for Google Apps Script automation and the clasp CLI - local development, time-driven triggers, the manifest and OAuth scopes, and calling Google services (Sheets, Admin SDK) as Advanced Services. Triggers: Apps Script, clasp, scheduled script, ScriptApp trigger, appsscript.json, advanced services.
license: MIT
metadata:
  author: Farz Owasil
  version: "1.0.0"
  domain: automation
  triggers: Apps Script, clasp, Google Apps Script, time-driven trigger, appsscript.json, advanced services, ScriptApp
  role: specialist
  scope: implementation
  output-format: script
  related-skills: google-workspace-admin, python-pro
---

# Apps Script Automation (clasp)

Google Apps Script automation and the clasp CLI for Corp IT / TechOps, typically lightweight automation and scheduled collectors over Workspace data (Sheets, Drive, Admin SDK).

## Corp IT / TechOps context

- Any generated `.gs` / `.js` carries a header comment with `Script Author: Farz Owasil`, a one-line purpose, prerequisites (scopes, advanced services), and the date.

## clasp and project files (verified)

- Stable across clasp v2 and v3: `clasp login`, `clasp push`, `clasp pull`.
- Version caveat: clasp v3 renamed several subcommands (`create` to `create-script`, `clone` to `clone-script`, `deploy` to `create-deployment`, `version` to `create-version`, `open` to `open-script`, `logs` to `tail-logs`). Check `clasp --version` and the clasp README before using those, and do not assume one set is universal.
- Project files: `.clasp.json` (project settings), `.claspignore` (push ignores), `.clasprc.json` (saved credentials), and `appsscript.json` (the manifest). The manifest declares `timeZone` and `oauthScopes`.

## Scheduling and Google services (verified)

- Time-driven trigger in code: `ScriptApp.newTrigger("fn").timeBased().everyHours(6).create()`. The ClockTriggerBuilder also offers `everyDays`, `onWeekDay`, `atHour`, `everyMinutes`, and similar.
- Admin SDK and Sheets are used as Advanced Google services: enable them first (editor "Add a service", or the manifest `dependencies.enabledAdvancedServices`), then call. Note that Google API `delete` methods are exposed as `remove` in Apps Script.

## Core workflow

1. Develop locally with clasp (`login`, then `pull` / `push`), keeping `appsscript.json` scopes minimal.
2. Enable only the advanced services you actually call.
3. Add a time-driven trigger for scheduled jobs.
4. Review OAuth scopes before deploy, least privilege.

## Guardrails

- clasp command names depend on the installed major version: verify against `clasp --version` and the README rather than asserting.
- Keep `oauthScopes` least-privilege.
- Do not invent Apps Script methods or advanced-service identifiers. Confirm each service's own reference before putting literal code in a script, and add the `Script Author: Farz Owasil` header to generated scripts.
