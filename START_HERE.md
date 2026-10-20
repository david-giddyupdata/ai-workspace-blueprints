# START HERE: instructions for the AI agent

_This file is written to the AI agent. If you're a person, you can read it too: it's what the agent will do. To
begin, open this folder in Claude Code (VS Code or the Claude desktop app) and type: "Read START_HERE.md and set this
workspace up for me."_

---

You are setting up this folder as a workspace for the person you're talking to. They may never have used an AI agent,
an editor or GitHub before. Follow these steps in order. Keep every message short and plain. Explain any technical
word the first time you use it.

## Ground rules for the whole setup

- **Ask before you create or change any file**, and say which file and why, in one line.
- **Never ask for a password, API key, account number or card number.** If they offer one, tell them not to paste it
  and don't write it anywhere.
- **Don't install anything, sign in to anything, buy anything, delete anything or go online.** None of it is needed.
  If you think something must be installed, stop and ask first, saying what it is and what it costs.
- **Work only inside this folder.**
- If a step doesn't work in the tool you're running in, say so plainly and offer the simplest alternative (for
  example, show the file's text so they can save it themselves). Don't guess at menu names.

## Step 1. Say hello and explain the permission prompts

In a few lines:

- Say what you're going to do: ask about five questions, write three files from the answers, then suggest a first
  project. About 15 minutes.
- Explain the permission prompts: "I'll ask before I create or change a file or run a command. Say yes when it's a
  file in this folder and you understand what I'm doing. Say no to anything that signs in, buys, deletes or installs.
  If you're not sure, say no and ask me."

## Step 2. Interview them, one question at a time

Ask these one at a time. Wait for each answer. Accept short answers; don't push for more.

1. What should I call you?
2. What's your role, and who is your work for? (one or two sentences)
3. Name one real project you'd like help with: a report you write every month, a procedure document, a set of
   slides, a set of instructions people follow. Real work beats practice work, because you can judge the result.
4. How do you like to work? (for example: short answers, plain language, ask before big changes, tell me plainly
   when my idea is a bad one)
5. What should I never do? (Suggest these as a starting list they can change: never sign in for you; never paste or
   save a password or key; never delete anything I didn't create unless you name it; never send, publish or pay for
   anything without your OK.)

## Step 3. Write `AGENTS.md`

`AGENTS.md` already exists in this folder as a template. Ask permission, then fill it in from their answers:

- Remove the "not set up yet" note at the top.
- Fill in "Who I am", "My project", "How I work" and "Ground rules". Use their words. Keep the whole file under one
  page.
- Keep the "Files in this folder" section as it is.

Then show them the result in a few lines and ask if anything is wrong. Fix what they say.

Leave `CLAUDE.md` alone: its one line tells Claude Code to read `AGENTS.md` every session.

## Step 4. Create `RULES.md` and `SESSION_HANDOFF.md`

Ask permission, then:

- Copy `use/templates/RULES.md` to `RULES.md` in this folder. Delete the template's comment block and its three
  example rules, then add their "never do" answers as the first rules (R1, R2, ...), each with their name, today's
  date and "Enforced by: Not built".
- Copy `use/templates/SESSION_HANDOFF.md` to `SESSION_HANDOFF.md` in this folder. Delete its comment block and fill
  in section 1 with "Workspace set up today" and their project.

Explain each file in one line:

- `RULES.md`: "Every time you correct me, tell me to add it here as a rule. You teach me once."
- `SESSION_HANDOFF.md`: "At the end of a session, tell me to update it. Next time, I read it and pick up where we
  left off. Chat history runs out; files don't."

## Step 5. Suggest one small first project

Suggest one small job, based on their project. If nothing better fits, suggest this one:

> Give me a set of instructions you or others follow (a procedure, a runbook, a how-to, a checklist). I'll test it
> step by step as if I were a brand-new person, and write `FINDINGS.md`: each step that is wrong, unclear or
> missing, why, and a suggested fix. Then you check what I found before changing anything.

Tell them that findings are leads, not verdicts: they decide which are real.

If they agree, ask them to put the instructions in this folder (or paste the text), then do the test. If the
instructions need a website or a program, test only what you can read, and list the rest as "needs checking by you".

## Step 6. Close

In a few lines:

- What's set up: `AGENTS.md`, `RULES.md`, `SESSION_HANDOFF.md`.
- Three habits: ask for a file, not an answer; turn every correction into a rule in `RULES.md`; end each session with
  "update SESSION_HANDOFF.md".
- Where to learn more: `GLOSSARY.md` (every tool from the talk, with costs), `use/workspace-blueprint/BLUEPRINT.md`
  (a longer step-by-step guide), and `use/settings/` (stricter settings for a company computer).
- Update `SESSION_HANDOFF.md` with what you did, after asking.
