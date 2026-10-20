# Rules: my decisions, one home each

<!--
How this file works:
- Every decision the agent must follow lives here once, numbered. Other files point to it ("see R3")
  and never restate it, so a rule can't drift between two copies.
- Numbers are never reused or renumbered. A new rule takes the next free number.
- When two rules disagree, the newer dated one wins. Mark the older one "Replaced by R<n>" rather than deleting it.
- Each entry has three parts: the rule, then who decided and when, then what enforces it.
  "Not built" means the rule stands but nothing checks it yet, so the agent must remember it.

The habit that makes this work: every time you correct the agent, ask it to write the correction here as a rule.
You teach it once.
Delete these comments when you start.
-->

## Hard limits

- **R1 <The rule, in one sentence.>** <Any detail needed to apply it.>
  *<Who decided>, <date>.* Enforced by: <a setting, a script, a check, or "Not built">.

## Style

- **R2 Inclusive date ranges say "through", not "to".** "January 2020 through December 2025". "To" can read as
  stopping before the last month.
  *Me, 2026-10-13.* Enforced by: Not built (the agent applies it when writing).

## Safety

- **R3 The agent never deletes what it didn't create.** It may delete only files or objects its own run made, or ones
  I name. Before any other deletion it lists what it would delete and waits for my OK, by name.
  *Me, 2026-10-13.* Enforced by: partly a "deny" rule for `rm -rf` in the agent's settings; mostly this rule. A
  deny rule matches one spelling of a command, so other ways of deleting rely on the agent following R3.

## Replaced rules

<!-- Move a rule here when a newer rule replaces it, with "Replaced by R<n> on <date>". -->
