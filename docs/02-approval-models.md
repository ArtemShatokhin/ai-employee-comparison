# How AI employee products gate a risky action

Every product on this shortlist says a person stays in control. The useful difference is what the product treats as risky, who writes that rule, and what happens to the agent's turn while it waits. Kortix is the open-source AI Operating System, and its answer is the most explicit of the group: the rule is a policy file, and the actions are named.

## Kortix: Allow, Ask or Block, decided per action

Kortix gives a connector action one of three policies. Allow runs it, Ask holds it for a person, and Block refuses it. The manifest names them `always_run`, `require_approval` and `block`, and the interface shows them as Allow, Ask and Block.

Rules are evaluated in [a fixed order](https://kortix.com/docs/connect/connectors), and the first match wins. Project-wide policies in `kortix.yaml` come first, and a connector rule cannot override them. The connector's own rules come next, then a `sensitive: true` flag that holds every remaining action including reads, then `default_mode`. That default is `allow_all`, which is why the setting deserves attention on day one. Set it to `risk` and reads run while writes and destructive calls wait.

A rule can also test the arguments of the call, which is the part most products do not publish:

```yaml
policy:
  default_mode: risk

policies:
  - match: gmail.send_email
    action: always_run
    conditions:
      - arg: to
        match: "*@example.com"
  - match: gmail.send_email
    action: require_approval
```

That example allows internal mail and holds everything else. A rule holds up to ten conditions, and all of them must match. A malformed condition fails closed, so a typo cannot open an action.

A held call returns a pending status with an approval link and a summary. Nothing runs. A person opens the request, sees the redacted arguments the provider will receive, and approves or denies with an optional note. The decision goes back into the session and the agent continues.

Three limits are worth knowing before a rollout. An approval covers one exact request, so a changed argument needs a new approval. The identical call runs without a second approval if it repeats within fifteen minutes. There is no session-wide approval, and an action that must run unattended needs an Allow rule. That last point is the cost of the model: autonomy at 3am is a decision you wrote down in advance.

Approval gates you set. Off until you set them. Per-resource permissions for people and agents. Roles, groups, and an audit trail.

## CellCog: a danger class the vendor defines

CellCog describes a two-level model. You set goals and permissions when you hire the role, and then a class of action waits for a person. The homepage says: "You set the permissions up front. You decide what they can do on their own, and anything dangerous waits for your approval." It adds: "Anything risky waits for your yes. It buys only what you approve."

That is clear about intent and quiet about mechanics. The page does not publish a per-action table, a rule syntax, or a list of which actions count as dangerous. A buyer can test the boundary in a trial, and cannot read it beforehand.

## Viktor: approval on the irreversible

Viktor draws the line at reversibility. The homepage says the agent "proposes the next step and asks before anything he can't undo", and lists "Approval buttons on anything irreversible. Per-person permissions and access controls." A separate line reads "Autonomous, not unsupervised."

The rule is easy to explain to a team, which is a real advantage for adoption. The trade-off is that the irreversible class is defined by the product, not by your risk register. A refund and an internal note may both be writes; only one needs a second pair of eyes, and the vendor decides where the button appears.

## Lindy: approval on outside impact

Lindy draws the line at whether an action leaves the workspace. Its pricing page says: "Anything with outside impact waits for approval such as sending an email, updating a ticket, posting to another channel, publishing a doc. Read-only lookups from approved sources do not require approval."

This is the cleanest read/write boundary of the three hosted products. It is also a blanket gate, with no documented per-action override, so a high-volume support queue and a quarterly report wait in the same way.

## What decides a rollout

Three things separate these models once a team runs them.

The first is authorship. On Kortix a policy is a file your security team can review and your platform team can diff. On the hosted products the boundary is a product decision, described in marketing language.

The second is granularity. "Anything irreversible" and "anything with outside impact" are classes. A rule that matches `gmail.send_email` with a condition on the recipient is an action, and an action is what a review process usually needs.

The third is what happens to the work. A held call on Kortix pauses one request and resumes the session after a decision. A blanket gate on a hosted product can stop a run and leave the agent without a documented resume path.

## A test to run in a trial

Pick one action that writes to a system of record and one that sends a message. Run both with a destination you control.

1. Confirm the action is held, and read the arguments the approver will see.
2. Change one argument and check that the product asks again rather than reusing the approval.
3. Repeat the identical call within the vendor's replay window and see what runs.
4. Start the same action from a schedule with nobody present, and confirm the product either blocks it or has a written rule for autonomy.

A product that passes all four has an approval model you can operate. A product that fails the third step will replay a decision you did not intend.
