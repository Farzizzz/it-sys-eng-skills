# IT & Systems Engineering Skills

A Claude Code skill pack for IT and Systems Engineering work in a Corp IT / TechOps setting. It bundles 19 skills across infrastructure, cloud, DevOps and SRE, identity, endpoint management, collaboration tooling, databases, observability, and code and security review.

Maintained by Farz Owasil.

## What is in the pack

19 skills. 15 are adapted from [jeffallan/claude-skills](https://github.com/jeffallan/claude-skills) (MIT) with light Corp IT / TechOps context added, and 4 are original IT administration skills.

### Infrastructure and cloud
- `terraform-engineer` - infrastructure as code across AWS, Azure, GCP (plan, review, approve, apply)
- `cloud-architect` - cloud architecture, migration, cost, disaster recovery
- `kubernetes-specialist` - workloads, RBAC, network policy, Helm, troubleshooting

### DevOps and SRE
- `devops-engineer` - CI/CD, containers, Kubernetes manifests, IaC templates
- `sre-engineer` - SLOs, error budgets, incident response, capacity planning
- `monitoring-expert` - metrics, logging, tracing, dashboards and alerting

### Identity and endpoint management
- `okta-admin` - Okta IAM: group rules, app assignments, SSO/SCIM, lifecycle (original)
- `intune-windows-admin` - Intune for Windows endpoints only (original)
- `mac-mdm-admin` - macOS endpoint management via Kandji (original)
- `google-workspace-admin` - Google Workspace and GAM administration (original)

### Databases
- `postgres-pro` - PostgreSQL tuning, replication, advanced features
- `sql-pro` - query optimisation, schema design, cross-dialect work

### Quality, security, and tooling
- `code-reviewer` - broad code review across correctness, performance, maintainability
- `security-reviewer` - security audits and vulnerability reports
- `secure-code-guardian` - secure implementation patterns, OWASP Top 10
- `debugging-wizard` - systematic root-cause debugging from errors and logs
- `python-pro` - typed, tested Python 3.11+
- `cli-developer` - building CLI tools
- `atlassian-mcp` - Jira and Confluence via MCP (JQL/CQL)

## Install

### From GitHub (once pushed)

Replace `YOUR_GITHUB_USERNAME` in `.claude-plugin/marketplace.json` with your GitHub handle, push the repo, then in Claude Code:

```
/plugin marketplace add YOUR_GITHUB_USERNAME/it-sys-eng-skills
/plugin install it-sys-eng-skills
```

### Individual skills (no plugin)

Copy any skill folder into `~/.claude/skills/`:

```
cp -R skills/okta-admin ~/.claude/skills/okta-admin
```

## Endpoint management split (hard rule)

macOS is managed by Kandji (`mac-mdm-admin`). Windows is managed by Intune (`intune-windows-admin`). The skills never mix the two: if a platform is not stated, they ask which it is before answering.

## Attribution

15 skills are derived from [jeffallan/claude-skills](https://github.com/jeffallan/claude-skills), used under the MIT License. Each derived skill retains an `upstream` reference in its frontmatter. The 4 identity and endpoint skills are original. See `LICENSE` for the full notice.

## Licence

MIT. See `LICENSE`.
