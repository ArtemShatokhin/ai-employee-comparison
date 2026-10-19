# Moving from a hosted AI employee to one you run

Relay.app shut down in September 2026, and its own homepage records the outcome: "All accounts, workflows, and run history have been permanently deleted." Nobody plans for that. A platform lead still has to assume it can happen, because the difference between a pause and a rebuild is whether the work product leaves with you. Kortix is the open-source AI Operating System, and this checklist turns that assumption into a migration a team can finish in two weeks.

## What you can export, and what you cannot

Three buckets matter, and only the first is easy. Sort every asset into one of them before you ask for the export.

- **Portable with an export.** Conversations, delivered documents and the text of prompts usually come out through a data export request or an API. Ask for it before you cancel, in a machine-readable format, and check that the export includes tool calls and not only messages.
- **Rewritable by hand.** Instructions, tool scopes, approval rules and schedules can be retyped and recreated from screenshots and notes. This is real work, and it is bounded.
- **Usually lost.** The vendor's memory index, its internal identifiers, the approval history and the accumulated state that made the agent feel like it knew the business. A memory folder you can open, as Lindy documents, changes this bucket. A memory store behind a settings page does not.

## Take an inventory first

Two days of inventory saves two weeks of surprise later. For each role, write down the person who owns it, the tools it reaches, the credentials behind those tools, the schedules it runs on, the data it touches and the audit obligation it carries. Then tag each item as portable, rewritable or lost.

That inventory is also the business case. A role with twenty tool grants and a daily schedule is a project. A role that drafts one weekly report is an afternoon.

## The checklist

**1. Create the project.** Install the CLI, run `kortix init` and then `kortix ship` to start the project repo. The repository is the migration target, so create it before you move anything.

**2. Write each role as a file.** One markdown file per role at `agents/<name>.md`, holding the instructions and the tone. Copy the prompt text from the old product, then edit it while you still have the old transcripts in front of you.

**3. Declare governance in `kortix.yaml`.** Each agent gets a block naming its file and its grants. Start narrow. The starter template grants everything to its default agent so a fresh project is capable, and a migrated role does not need that.

**4. Rebuild tool access as connectors.** 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP. Use a managed app where one exists, and an MCP server or OpenAPI document for the rest. Keep the credential in the project secret store and grant it to the agent that needs it.

**5. Move the memory into files.** Write the stable facts into files under `memory/`: pricing exceptions, naming rules, escalation paths, the customers who need a call before a shipment. Summaries written by a person beat an exported index, because the summary is the thing you can review.

**6. Set the policy before the first run.** Run `kortix connectors policy set --default risk` so reads run and writes wait, then add explicit Allow rules for the unattended jobs. Approval rules you cannot write down are rules you should not run.

**7. Recreate schedules.** A cron trigger replaces a vendor schedule. Each trigger names the agent it runs as and carries the prompt template, so a morning report is a trigger plus a role file.

**8. Run in shadow for two weeks.** Keep the old product live and send it the same work through a small test channel. Compare output on the tasks that matter. Do not cut over on a good demo.

**9. Cut over, then keep the old account read-only for thirty days.** Forward the channels, announce the new inbox, and leave the old account open long enough to answer questions about what it did. Session work reaches `main` through a change request. Merge is default-deny for agents. That gate is new for a team coming from a hosted hire, and it is the point.

**10. Review the first month of audit, then close the account.** Check the actions you expected, the approvals that held, and the ones that surprised you. Close the old account with the export already downloaded and stored somewhere you control.

## What has to be rewritten

Schedules change shape, because a cron expression and a vendor's scheduling UI do not map one to one. Approval policy changes most: a hosted product that treats every write as risky becomes a set of named rules, and someone has to decide which calls run unattended.

Integrations also need a decision. A tool with a managed connector takes minutes. A tool without one needs an OpenAPI or MCP wrapper, and that is a small engineering task.

## A two week schedule

Days one and two cover the inventory. Days three to five write the role files. Days six to eight rebuild connectors and secrets. Days nine and ten set policy and start the shadow run. The second week runs both systems in parallel, fixes the gaps, and cuts over on the Friday, with the old account read-only until the end of the month.

## What you get on the other side

One isolated sandbox per session. Each session has its own isolated machine and branch. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. The role files, the grants and the memory are in a repository you can clone, which means the next migration is a `git clone`, and the next vendor decision is optional.
