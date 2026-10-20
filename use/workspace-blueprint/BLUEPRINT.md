# Build your own agent environment: a step-by-step guide

By David Baldwin, GiddyUp Data LLC. Version 0.2, October 2026.

**In a hurry?** The starter kit's [`START_HERE.md`](../../START_HERE.md) has your agent do Steps 1.1 and 1.2, plus
the rules file and the handoff, in about 15 minutes. This guide is the longer path.

This guide walks you through building a small environment where an AI agent does real work for you, while you stay
in charge. You don't need to know how to program. You need one real project, an agent tool, and a few hours spread
over a week.

**Want a coach?** Paste [`TUTOR_PROMPT.md`](TUTOR_PROMPT.md) into your favorite chatbot (Claude, ChatGPT, Gemini or
similar), then attach or paste this guide. The chatbot will take you through it one step at a time and wait for you
before moving on.

---

## Before you begin

### Chatbot, agent, environment: what's the difference?

- A **chatbot** answers questions. You copy its answer somewhere and do the work yourself.
- An **agent** acts. It can read and write files, run programs, drive a web browser and ask other AI models for help.
- An **environment** is the setup around the agent: the files it reads every time, the tools it can reach, the rules
  it must follow, the checks on its work, and the points where you approve. A good environment is what turns a
  clever agent into a dependable one.

This guide builds the environment in six parts. (The talk's mind map groups the same ideas into five branches:
Workspace, Memory, Hands, The team and Boundaries. Foundation and You, as editor, sit under Workspace and Memory;
Checks sit under The team.)

| Part | What it is | Why it matters |
|---|---|---|
| 1. Foundation | The source material everything is built from: templates, reference documents, your past work | Get it right once and many outputs follow from it |
| 2. Hands | The ways an agent operates tools: a browser, a service's API, a plug-in, a file | Without hands, the agent can only talk |
| 3. Boundaries | What the agent may do on its own, and where you step in | You hand over real work without handing over everything |
| 4. A team of models | One AI that coordinates, and others that check or specialize | No single model is best at everything |
| 5. Checks | AI reviewing AI work, and the work tested against reality | Catches output that looks right but isn't |
| 6. You, as editor | You set direction, review and approve | Your expertise moves from typing to judging |

### What you need

| Item | Cost (October 2026; check before you buy) |
|---|---|
| A chatbot to coach you (optional) | Free tiers work |
| An agent tool, such as **Claude Code** (from Anthropic, runs inside the free Visual Studio Code editor or the Claude desktop app) | Claude Code needs a paid Claude plan, from about $20 a month |
| One real project you care about: a report you write every month, a procedure document, a set of slides, a course | Yours |

Nothing in this guide requires the paid video tools in the worked examples. The full cost list is in
[`BEFORE_YOU_START.md`](../../BEFORE_YOU_START.md).

### How each step works

Every step has the same shape:

- **Do this:** the action, in plain words.
- **You should see:** how you know it worked.
- **Why it matters:** the idea behind it, so you can adapt it.

Steps marked **Ask your agent** include text you can paste into your agent tool's chat. Change the words in
angle brackets, such as `<my project>`, to fit you.

Short boxes marked **My example** show how I applied the step in my own business. You don't need to copy them.

---

## Step 0. Decide: buy, configure or build

**Do this:** before you build anything, decide which of three paths fits the job.

| Path | What it means | When it wins |
|---|---|---|
| **Buy** | Use a managed agent product from a vendor. Some give the agent its own computer in the cloud and say they ask before consequential actions | One-off or routine web tasks, when the vendor's limits are good enough for you. Treat each vendor's safety claims as claims, dated, until you've checked them |
| **Configure** | Take an agent tool you already have and give it a template, a rules file and a check | Most people, most of the time. This is what this guide does |
| **Build** | Write custom connections and checks, like my video pipeline | Only when you have a real need, someone who will own it, and a budget to keep it running |

**You should see:** a one-line answer to "which path, and why?" For this guide, the answer is "configure".

**Why it matters:** building is fun, and it creates something you have to maintain forever. Start with the smallest
setup that does the job.

---

## Part 1. Foundation

### Step 1.1 Pick one real project

**Do this:** choose one piece of work you already do and know well. Make one folder for it on your computer, and open
that folder in your agent tool.

**You should see:** your agent tool showing the folder, empty or with your existing files in it.

**Why it matters:** an agent is only as good as what you can judge. On work you know, you'll spot its mistakes at once.
Practice projects teach you less, because you can't tell good output from plausible output.

### Step 1.2 Tell the agent who you are

**Do this:** fill in [`AGENTS.md`](../../AGENTS.md) (or copy [`../templates/ABOUT_ME.md`](../templates/ABOUT_ME.md)
into it): who you are, how you want the agent to work, your tools, and things it must never do. Keep it at the top of
your project folder, where your tool reads it every session:

- **Claude Code:** reads `CLAUDE.md`. Make it one line, `Read @AGENTS.md first.`, so you keep one copy (the starter
  kit already has this file).
- **Other tools:** many read `AGENTS.md` directly. If yours doesn't, look for "project instructions", "custom
  instructions" or "rules" in its settings.

**Ask your agent:**

```text
Read my AGENTS.md and tell me in three lines how you will work with me.
Then tell me one thing in it that is unclear.
```

**You should see:** a short summary that matches what you wrote, and one fair question.

**Why it matters:** without this file, every session starts from zero and you repeat yourself. With it, you say
things once.

### Step 1.3 Make your structure the contract

**Do this:** write down the fixed structure of the thing you produce: the sections, in order, and what each one must
contain. Save it in your folder as `TEMPLATE.md`. If you already have a template (a Word document, a slide master),
put a copy in the folder.

**Ask your agent:**

```text
Here is a finished example of my work: <file name>. List its sections in order and describe what each one contains.
Write that as TEMPLATE.md. Don't change the example.
```

**You should see:** a list of sections you recognize. Fix anything it got wrong; you are the authority here.

**Why it matters:** a fixed structure gives the agent a predictable job, filling each section to a known standard, and
gives you a predictable review, because you know where to look.

> **My example:** every exercise in my course manual has the same parts: Instructions, Completed Results, Commentary
> and Extra Credit, with steps on the left and a screenshot on the right. That template is older than AI. The agents
> work inside it.

### Step 1.4 Ground the agent in real sources

**Do this:** put the reference material the work depends on into a `sources/` folder: vendor documentation, policies,
data dictionaries, last year's version. Tell the agent to use these files for facts, not its memory.

**You should see:** a `sources/` folder with real files, and a line in your `AGENTS.md` such as
"For facts, search the files in sources/ and say which file you used."

**Why it matters:** an AI's memory is out of date and sometimes invented. Files you chose are current and checkable.
Even better, test against the real thing (Part 5): the documentation describes the product, but the product is the
truth.

### Step 1.5 Show your style instead of describing it

**Do this:** put two or three examples of your own best work in a `style-examples/` folder.

**Ask your agent:**

```text
Study the files in style-examples/. Describe my style in ten bullet points: tone, length, layout, word choices,
what I never do. Save it as STYLE.md. I'll correct it.
```

**You should see:** a style description that sounds like you. Correct it until it does.

**Why it matters:** describing a style is hard; showing it is easy. The agent can match examples better than it can
follow adjectives.

> **My example:** I spent years making screenshots by hand, with orange boxes, numbered circles and torn edges. The
> agent studied those and now produces pictures in the same style from code.

### Step 1.6 Never edit the master

**Do this:** keep one master copy of anything important that the agent must not change. Name it clearly, such as
`MASTER - <name>`, and add a rule: "Never edit files whose names start with MASTER. Work on a copy."

**You should see:** the rule in your instructions file, and the agent working on copies.

**Why it matters:** if the master stays clean, any mistake is undone by making a fresh copy. A change becomes a re-run,
not a repair.

> **My example:** scripts rebuild my 317-page draft manual from the master every time. When I changed the torn-edge
> style, 244 pictures re-rendered in about 20 seconds. Machine time, not review time: I still review.

---

## Part 2. Hands

### Step 2.1 Ask for the artifact, not the answer

**Do this:** next time you'd ask a chatbot a question, ask your agent for the finished thing instead: the file, the
page, the spreadsheet, the draft email saved as a file.

**Ask your agent:**

```text
Don't explain how to do this. Do it: create <file name> in this folder with <what it should contain>.
Tell me when it's saved, and what you weren't sure about.
```

**You should see:** a new file in your folder, plus a short note of its doubts.

**Why it matters:** this is the whole shift. A chatbot gives you words to act on; an agent gives you work to review.

### Step 2.2 List the tools, and how the agent reaches each one

**Do this:** list the tools your project touches (a website, a spreadsheet, an email account, a design app). For each
one, write down how an agent could reach it. There are four ways in:

| Way in | What it means | Upkeep | What can go wrong |
|---|---|---|---|
| **API** | The service's front door for programs | Low: vendors keep it stable | Keys to guard; usage bills |
| **File handoff** | The agent writes a file the app opens (a spreadsheet, a document, an import file) | Low: file formats change slowly | The least control |
| **Plug-in or bridge** | Code inside the app takes the agent's commands | High: you own it, and app updates can break it | It runs with your rights on your computer |
| **Browser** | The agent clicks through the website like a person | Highest: screen changes break it, and it's slow | Once you're signed in, it acts as you; it may break the site's terms |

Rule of thumb: prefer the API. If there's no API, hand off a file. Build a bridge only when you need the control and
will own the upkeep. Drive a website last, and only where its terms allow it.

**You should see:** a short table, one row per tool, with the way in you'll use.

**Why it matters:** an agent can only do what it can reach. Choosing the way in is a business decision about upkeep
and risk, not just a technical one.

> **My example:** my video editor (Adobe Premiere Pro) had no way in that did what I needed, so the agent built a small
> bridge that only takes commands from my own computer. That's the "build" path, and I own its upkeep now.

### Step 2.3 Give the agent its own browser, and sign in yourself

**Do this:** if the agent will use websites, give it a separate browser profile, never your everyday one. Sign in to
each site yourself. Add a rule: "Never type my passwords. If a sign-in page appears, stop and tell me."

**You should see:** a second browser window, with its own profile, that the agent uses.

**Why it matters:** this keeps the agent away from your other accounts. It is separation, not a sandbox: once you've
signed in, that browser can act as you on that site. Part 3 covers what that means.

---

## Part 3. Boundaries

### Step 3.1 Write down what the agent may do alone

**Do this:** make three short lists in your instructions file:

- **Do without asking:** for example, read files in this folder, create new files, make drafts.
- **Ask me first:** for example, change an existing file, run a program, install anything, spend money.
- **Never:** for example, sign in for me, send or publish, delete what you didn't create, paste keys into a chat.

**You should see:** the three lists in your `AGENTS.md`.

**Why it matters:** you can hand over real work only when you know where it stops. Written limits also make the
agent's behavior easier to predict and to review.

### Step 3.2 Keep the permission prompts on

**Do this:** leave your agent tool's default setting, where it asks before it edits files or runs commands. Say yes
only when you understand what it's about to do. At a company, start with the stricter settings in
[`../settings/`](../settings/README.md) and talk to your IT or security team.

**You should see:** the agent pausing to ask before it changes things.

**Why it matters:** prompts are slow, and that is the point. Many tools let you switch them off. Keep the permission
prompts on. On my own computer I run with them off and rely on habits instead; that describes my setup, it isn't a
recommendation. At work, follow your company's rules. An agent with prompts off can do anything your user account can
do.

### Step 3.3 Keep keys out of files and chats

**Do this:** if the agent needs a password or an API key, keep it in a password manager, your operating system's
keyring or a secrets manager, never in a chat and never in a file in your project folder. Ask your agent to read it at
the moment it's needed.

**You should see:** no keys anywhere in your project folder or chat history.

**Why it matters:** chat logs and files get copied, synced and shared. A key in either one is a key you've given away.

### Step 3.4 A person on every step that can't be undone

**Do this:** list the irreversible actions in your project: paying, sending, publishing, deleting. For each one,
decide that you do the last click. Add the rule "The agent may delete only what its own work created, or what I name."

**You should see:** a short list, and the rule in your instructions file.

**Why it matters:** most mistakes can be fixed. These can't. Keep a human on them.

> **My example:** in October 2026, an agent bought event tickets for me. I started it from my phone, and it browsed on my
> desktop. I typed the card number and clicked Pay myself. That checkpoint was my choice; nothing forced it.

### Step 3.5 Know the difference between mistakes and attacks

**Do this:** read your safeguards from Steps 2.3 to 3.4 again, and sort them into two columns:

- **Mistake prevention** stops an honest agent's accident: separate browser, prompts on, create but don't delete, a
  person on payments. These work well.
- **Protection from attack** stops someone trying to misuse your agent. Most personal setups have very little.

Then learn the name of the main threat: **prompt injection**. A web page, email or document can hide instructions,
and an agent that reads it may follow them as if they came from you. **It is not solved.** No current defense fully
prevents it ([OWASP](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)). If the agent is signed in to a site
and gets fooled, it acts with your sign-in.

**You should see:** two columns, and an honest "very little" under the second one.

**Why it matters:** knowing which safeguards stop what keeps you from trusting the wrong one. The practical defense
is to keep the agent away from data and accounts it doesn't need, and to confirm anything consequential yourself.
Real isolation is a separate virtual machine with no sign-ins, which is a step for later, or for your IT team.

### Step 3.6 Check the terms before you automate a website

**Do this:** before an agent drives any website for you, read that service's terms of use on automation.

**You should see:** a yes, a no or "ask them" next to each website on your Step 2.2 list.

**Why it matters:** technically possible is not the same as permitted. Breaking a service's terms can cost you the
account.

### Step 3.7 Verify your safeguards; don't just remember them

**Do this:** test each safeguard you're relying on. Ask the agent to try something harmless that a rule should stop,
and check that it stops.

**Ask your agent:**

```text
Read my rules. For each "Ask me first" and "Never" rule, tell me what actually enforces it: a setting in this tool,
or only your instructions. Then list any rule that nothing enforces.
```

**You should see:** a list that tells you which limits are real settings and which are only promises.

**Why it matters:** a rule that nothing enforces is only a promise, and a safeguard you haven't tested is a hope.
The test tells you which of your limits are real.

---

## Part 4. A team of models

### Step 4.1 Separate the maker from the checker

**Do this:** when your agent finishes something that matters, have a different AI review it: a fresh session that
didn't do the work, or a model from another company. Give the checker the work and your rules, not the maker's
explanation.

**Ask your agent (or a fresh chat):**

```text
You did not write the attached work. Review it against my rules in RULES.md and STYLE.md.
List each problem with where it is and why it's a problem. Don't fix anything.
```

**You should see:** a list of specific problems, some you agree with and some you don't.

**Why it matters:** in business this is called separation of duties. The one who makes the work shouldn't be the only
one who checks it. A second model catches things the first one is blind to.

### Step 4.2 Treat findings as leads, not verdicts

**Do this:** for each problem the checker raises, decide yourself: real, not real, or not sure. Fix only the real
ones. Ask the maker to check any finding against the work before it changes anything.

**You should see:** a shorter list of real problems than the checker reported.

**Why it matters:** more models give more opinions, not proof. A checker is worth having for what it tests against
reality, not for how confident it sounds.

> **My example:** for each video, a model from a different company reviews the frames without seeing my notes. On one
> round it found six of my eight notes, plus 31 real issues I hadn't noted. About a quarter of what it reported was
> wrong. That's one video's result, not a ranking.

### Step 4.3 When you aren't sure which model is best, test them

**Do this:** give two or three models the same small task, and score the results against your own standard.

**You should see:** a short table: model, what it produced, whether you'd use it, what it cost.

**Why it matters:** the best model for one job is often not the best for another, and prices differ a lot.

> **My example:** five models built the same twelve animated pieces for a video. The cost per piece I kept ranged from
> about 13 cents to about $2.85. Same job, a twenty-fold difference.

---

## Part 5. Checks

### Step 5.1 Treat a document as a script you can run

**Do this:** pick a document that describes steps: a procedure, a how-to, an onboarding guide, a runbook. Have the
agent follow it exactly, one step at a time, on a test copy or a test account, and log every place where the
document and reality disagree.

**Ask your agent:**

```text
Follow <document> exactly, step by step, as a brand-new user would, using only what the document says.
Work only in <test copy or test account>. For each step, record: what the document says, what you actually saw,
and whether it is Wrong, Unclear or Polish. Stop and ask me before anything that signs in, sends, buys or deletes.
Save the log as CHECK_LOG.md.
```

**You should see:** a log with three columns: the document says, what the agent saw, and a label.

**Why it matters:** any written procedure can be tested this way, and the log is evidence. This is one of the most
useful things an agent can do, and it works for any profession.

> **My example:** an AI playing a brand-new student, with only screenshots, a mouse and a keyboard, walked my whole
> course manual overnight in the live product: 17 runs, 1,662 actions, 341 findings. Before I trusted it, I tested it
> on one exercise with 15 problems I already knew about. It found 12, so I knew it misses some.

### Step 5.2 Check the checker

**Do this:** before you rely on a new check, try it on something where you already know the problems. Count how many
it finds and how many it misses. Then, for every finding on real work, confirm it yourself before you act.

**You should see:** a simple score, such as "found 12 of 15", and a list of findings you confirmed.

**Why it matters:** an unchecked check gives false comfort. One "blocker" my AI student reported turned out to be its
own clumsy mouse drag.

### Step 5.3 Review only what changed

**Do this:** when you review a new version, compare it with the version you last approved and look only at the
differences. Ask the agent to build that comparison for you.

**Ask your agent:**

```text
Compare <new version> with <last approved version>. Show me only what changed, side by side, with a one-line reason
for each change. Set aside anything that changed in the file but looks the same.
```

**You should see:** a short list of real changes instead of the whole document.

**Why it matters:** you can't re-read everything after every change. After one rebuild of my manual, 197 picture
files had changed, but 155 were only re-saved and looked the same. I reviewed the 42 that really changed.

### Step 5.4 Measure what you can

**Do this:** for anything that can be checked by counting or rules (word counts, required sections, dates in the right
format, numbers that must add up), ask the agent to write a check that runs every time.

**You should see:** a check you can run with one request, such as "run the checks", and a pass or fail for each rule.

**Why it matters:** a measured check doesn't get tired and doesn't guess. Save model reviews for judgment.

---

## Part 6. You, as editor

### Step 6.1 Turn every correction into a rule

**Do this:** copy [`../templates/RULES.md`](../templates/RULES.md) into your folder. Every time you correct the agent,
ask it to add the correction as a numbered rule, with the date. Tell it to read `RULES.md` every session.

**Ask your agent:**

```text
Add what I just told you to RULES.md as a new numbered rule, with today's date and one short example.
Then apply it to the work you just did.
```

**You should see:** `RULES.md` growing by one rule each time you correct something.

**Why it matters:** you teach it once. Over time the corrections get rarer and the rules get longer. That file becomes
your style, written down.

> **My example:** my course manual has 18 review rules, such as "inclusive date ranges say 'through', not 'to'". My
> video project has about 240.

### Step 6.2 End every session with a handoff

**Do this:** copy [`../templates/SESSION_HANDOFF.md`](../templates/SESSION_HANDOFF.md) and
[`../templates/NEXT_SESSION_PROMPT.md`](../templates/NEXT_SESSION_PROMPT.md) into your folder. At the end of each
session, ask the agent to update them.

**Ask your agent:**

```text
We're stopping. Update SESSION_HANDOFF.md with where things stand, what's next and anything open.
Then write NEXT_SESSION_PROMPT.md so a fresh session can pick up from here.
```

**You should see:** two files that would let a stranger pick up the work.

**Why it matters:** chat history runs out; files don't. The next session starts in two minutes instead of twenty.

### Step 6.3 You approve what goes out

**Do this:** make it a rule that everything the agent writes is a draft until you approve it, and that you send or
publish it yourself.

**You should see:** the rule in your instructions file.

**Why it matters:** your expertise moves from typing to judging. You remain accountable for what goes out, so you
should be the one who lets it out.

### Step 6.4 If you use your voice or face, get it right and get consent

**Do this:** if you want narration in your own cloned voice or a video avatar of yourself, use a service that
requires your consent, use only your own voice and likeness, and expect to invest real recording time.

**You should see:** the service's consent step completed, in your own name.

**Why it matters:** a quick clone is easy and rough; one good enough for paid work takes effort. Your likeness can
also be misused, so treat the recordings like a key.

> **My example:** my voice clone was trained on about two hours of usable audio. The avatar service had me record a
> consent statement on camera.

### Step 6.5 Keep a "not yet" list

**Do this:** keep a short list of jobs the AI couldn't yet do well enough for you. When a new model comes out, retry
them.

**You should see:** a list with dates.

**Why it matters:** the tools improve quickly. But credit your environment too: a better setup often helps as much as
a better model, and it carries over to the next model.

---

## Your first week

| Day | What to do | Steps |
|---|---|---|
| 1 | Pick the project, make the folder, write your instructions file | 0, 1.1, 1.2 |
| 2 | Add your template, sources and style examples; protect the master | 1.3 to 1.6 |
| 3 | Ask for three artifacts instead of answers; list your tools and ways in | 2.1 to 2.3 |
| 4 | Write your boundaries; check keys, irreversible steps and terms | 3.1 to 3.7 |
| 5 | Have a second model review one piece of work; run one document as a test | 4.1, 4.2, 5.1 |
| Every day | Turn corrections into rules; end with a handoff | 6.1, 6.2 |

## Three things to try tomorrow

- Ask for a file, a script or a page instead of an answer.
- Write your next five corrections into a rules file your AI reads every time.
- Have an AI test your instructions the way a brand-new user would. Then check what it finds before you act on it.

## Words used in this guide

| Word | Meaning |
|---|---|
| Agent | An AI that can take actions (read and write files, run programs, use a browser), not just answer |
| Agent tool | The program you use to run an agent, such as Claude Code |
| API | A service's front door for programs, so software can use it without clicking through the website |
| Instructions file | A file the agent reads at the start of every session, such as `AGENTS.md` or `CLAUDE.md` |
| Master | The original copy that is never edited; everything else is rebuilt from it |
| Permission prompt | The agent tool asking "may I?" before it edits a file or runs a command |
| Prompt injection | Hidden instructions in a web page, email or document that an agent may follow as if they came from you |
| Sandbox | An isolated space where a program can't reach the rest of your computer or accounts |
| Subagent | A helper agent the main agent starts for one job, such as a review |

## Where to go next

- [`../templates/`](../templates/): the starter files used in this guide.
- [`../settings/`](../settings/README.md): stricter agent settings for a company computer.
- [`../../GLOSSARY.md`](../../GLOSSARY.md): every tool from the talk, one line each, with costs.
- My own pipelines, to see how the parts fit together in working code (they won't run unmodified on your computer):
  [ai-documentation-pipeline](https://github.com/david-giddyupdata/ai-documentation-pipeline) and
  [ai-video-pipeline](https://github.com/david-giddyupdata/ai-video-pipeline).
