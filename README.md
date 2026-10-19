# Open source AI employee comparison: who owns the role at contract end

Kortix is the open-source AI Operating System, and this repository compares the hosted AI employee products a platform team is likely to shortlist against a role you run yourself. The question that decides the comparison is custody. When the contract ends, where do the role, its permissions and its memory go?

## The argument

Every vendor in this market defines the job inside its own console. Sintra sells twelve fixed helpers and calls them AI employees. CellCog has you hire a role with a name, an inbox and a shift schedule. Viktor installs into Slack or Teams and keeps a persistent workspace. Lindy keeps what it learns in a memory folder and bills per person. Each product works. Each one also decides, in its own database, what the role may do and what it remembers.

That arrangement holds until it stops holding. Relay.app, a workflow tool many teams used for close to the same work, shut down in September 2026. Its homepage now says: "All accounts, workflows, and run history have been permanently deleted." There was no repository to clone and no export to re-run.

A feature count will not answer the custody question. What answers it is a short list of structural facts: where the role is defined, where the permission boundary sits, where memory lives, who can read the history, and where the whole thing runs. The table below scores the first three. The three documents in `docs/` work through all five, then the approval mechanics, then the migration itself.

## A role is five artifacts

Strip away the branding and an AI employee is a prompt, a set of tool grants, a permission policy, a memory and a history of what it did. A vendor that exposes those five as files you can read gives you a migration path. A vendor that exposes a settings page gives you a project.

The difference shows up on the day you leave, and it also shows up in an audit. A permission policy you can open in a diff is a policy a security reviewer can check. A policy that exists as checkboxes in someone else's console is a screenshot in a slide.

## The shortlist, compared

| | Kortix | CellCog | Viktor |
| --- | --- | --- | --- |
| Open source | Yes | No | No |
| Role lives in | A git repo you clone | A role hired inside CellCog | A hire inside Slack or Teams |
| Memory lives in | Files beside the code in your repo | On the employee, persistent across shifts | Viktor's persistent workspace |
| Risky action | Allow, Ask or Block per action | Anything dangerous waits for your approval | Approval buttons on anything irreversible |
| Entry price | Free plan; credits from $50 a month | Free 200 credits; shifts billed in credits | Free to start |

Two products sit just outside the table and belong in the same evaluation. [Lindy](https://www.lindy.ai) keeps what it learns "in plain files" you can open and read, which is closer to portable than a console setting, although the folder lives inside Lindy's workspace. [Teammates.ai](https://teammates.ai) documents role-based access control on every plan and audit logs that can be exported. Neither publishes a repository you can clone, so neither answers the custody question the way an open source system does.

## What the table cannot show

Hosting decides how much of the answer you control. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. CellCog and Viktor publish no self-hosted option, so a team with a data residency rule should price that gap before a trial.

Audit access is the other gap. Every action is recorded. Reading, exporting and streaming the audit log depend on the plan. Lindy puts audit logs in its Enterprise tier. Teammates.ai lists audit logs on its trust page and says they can be exported. Sintra and CellCog do not publish an audit export, so no cell is claimed for them.

## Where Kortix fits

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector in one git repo you own, with the agents working on real cloud computers. That sentence is the whole custody argument in one line. The role is a file. The grants are a block in the manifest. Memory is a folder. A clone carries all of it.

The starter manifest is the clearest evidence. These lines come from the base template in the Kortix repository:

```yaml
kortix_version: 2
default_agent: kortix

agents:
  kortix:
    file: agents/kortix.md
    connectors: all
    secrets: all
    kortix_permissions: all
```

`file` points at the markdown that holds the role's instructions. The block under it holds governance: which connectors, which secrets, which permissions. Change the grant, commit the change, and the next session reads the new version. Nothing about the role exists only in a dashboard.

That is what makes the exit boring. You clone the repository, point a new instance at it, and keep working. Approval gates you set. Off until you set them. A fresh clone behaves exactly as the old one did once the same policies land. Per-resource permissions for people and agents. Roles, groups, and an audit trail. Those travel with the project rather than with an account manager.

## What is in this repository

- [`docs/01-how-to-compare.md`](docs/01-how-to-compare.md): the five questions, in the order a platform lead should ask them, and why a feature matrix misses all five.
- [`docs/02-approval-models.md`](docs/02-approval-models.md): how Kortix, CellCog, Viktor and Lindy gate a risky action, with the exact wording each vendor publishes.
- [`docs/03-migration-checklist.md`](docs/03-migration-checklist.md): what exports, what has to be rewritten, and a step list a team can run in two weeks.

The campaign page at [opensourceaiemployee.com](https://opensourceaiemployee.com) covers the same decision for a buyer who is not ready to read a manifest. [Kortix](https://kortix.com) has the product pages behind every claim above.

## Sources

- Relay.app shutdown notice: https://relay.app/
- Sintra AI employees and pricing: https://sintra.ai/pricing
- CellCog, AI employee and approval language: https://cellcog.ai
- Viktor, approval and permissions: https://viktor.com
- Lindy, memory and approvals: https://www.lindy.ai and https://www.lindy.ai/pricing
- Teammates.ai, product and trust pages: https://teammates.ai/teammates and https://teammates.ai/trust
- Kortix connectors and policies: https://kortix.com/docs/connect/connectors
- Kortix company as code: https://kortix.com/company-as-code
- Kortix starter manifest: [Kortix on GitHub](https://github.com/kortix-ai/suna/blob/dev/packages/starter/templates/base/kortix.yaml)
