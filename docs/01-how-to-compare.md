# How to compare AI employees without a feature matrix

A feature matrix tells you which product has a Slack connector. It cannot tell you what you still own after the contract ends. Kortix is the open-source AI Operating System, and it answers that custody question in a way a hosted product structurally cannot, because the role is a file in a repository you can clone. This document gives you the five questions that surface the difference, in the order a platform lead should ask them.

## Start with the roster, then look past it

The products on this shortlist describe the job in their own language. [Sintra](https://sintra.ai/pricing) sells twelve helpers with names and fixed specialties. [Teammates.ai](https://teammates.ai/teammates) ships three named teammates, Raya for support, Adam for sales and Sara for recruiting, that share context. [CellCog](https://cellcog.ai) lets you hire a general-purpose role with its own inbox and shift schedule. [Lindy](https://www.lindy.ai) positions one teammate for a whole team. [Viktor](https://viktor.com) installs into Slack or Teams and calls itself a hire.

The roster is the easy part to read. The harder part is finding the sentence that says where the roster is stored.

## 1. The role must exist as a file

Ask for the file. Ask to see the instructions, the tool grants and the model choice in one place, outside the vendor's dashboard. If the answer is a settings page, the role is a row in someone else's database.

In Kortix an agent is a markdown file at `agents/<name>.md`, and its governance sits in the `agents.<name>` block of `kortix.yaml`. The behavior lives in the file, the grants live in the manifest, and both live in the project repo. Open source. Read it, fork it, audit it. That is a literal description of the exit path.

A vendor with a fixed roster may still produce good work. The risk is that the role's definition and the roster are the same object, so you cannot keep one and leave the other.

## 2. The permission boundary must be readable

Permissions have two halves. The first is who inside your company may run the agent, and the second is what the agent may reach. Ask to see both as data.

Teammates.ai documents role-based access control on all plans, with permissions at team, department and organization level. Viktor documents per-person permissions and access controls. CellCog says you set the goals and permissions up front. Lindy gates actions and adds SSO at Enterprise.

Connector credentials are brokered server-side and never enter the machine, so a tool grant does not hand the agent a raw key it can print. The policy that decides what a call may do is a file in the same repo.

## 3. Memory decides the exit cost

Memory is the asset that makes a replacement expensive. If the agent has learned your pricing exceptions, your naming rules and the three customers who need a call before a shipment, that knowledge is the product.

Lindy comes closest of the hosted products here: it says what it learns lives in plain files, and you can open the memory folder and read it. CellCog promises persistent memory where nothing resets, tied to the employee. Viktor keeps a persistent workspace. Teammates.ai says its teammates share memory and context natively.

Each of those is a real capability. Each also keeps the memory inside the vendor's workspace. In Kortix, memory sits beside the code as files in the project, so a clone carries the memory with the role and the history.

## 4. The history must be exportable

An audit trail is what lets you answer a question six months later: which agent sent that email, with which arguments, under whose approval. Ask whether the log is on by default, who can read it, and whether you can export it.

Every action is recorded. Reading, exporting and streaming the audit log depend on the plan. Lindy includes audit logs in Enterprise, and Teammates.ai lists audit logs it says can be exported. Sintra and CellCog do not publish an audit export, which is itself a useful finding for a regulated buyer.

## 5. Hosting sets the floor

The last question decides how much of the previous four you control when a vendor changes direction. Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free. CellCog and Viktor publish no self-hosted deployment, so a residency requirement moves into procurement.

## Why a feature matrix misses all five

A matrix scores presence. It records that a product has an inbox, and leaves out who owns the inbox's contents. It compares thirty rows of capabilities that change every quarter, and skips the five structural facts that decide whether you can leave.

The five questions also survive a product update. A vendor can rename a tier or add a model without changing where it stores your role. That is why this method stays useful after the feature list goes stale.

## A scoring sheet for a demo

Ask each vendor for the same five things and mark a clear pass or fail. Vague answers count as a fail.

1. A link to the role definition, readable without a login.
2. A permission policy you can read as a list of rules.
3. A memory export in a format you can open.
4. An audit export, or a written statement of when it is available.
5. A hosting option that matches your residency rule.

One fail means a rewrite at exit. Two or more means the role is rented, and the price should reflect that. The next document takes the second question apart, because approval behaviour is where the products differ most and where marketing language hides the mechanics.
