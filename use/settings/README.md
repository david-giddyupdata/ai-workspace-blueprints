# Stricter agent settings for a company computer

`claude-code-stricter.settings.json` is a starting point for running Claude Code on a work computer. Take it to your
IT or security team; it is meant to start that conversation, not to replace it.

## How I run

Keep the permission prompts on. On my own computer I run with them off and rely on habits instead; that describes my
setup, it isn't a recommendation. At work, follow your company's rules. (Off, for me, means Claude Code's
`bypassPermissions` mode; the habits are the blueprint's boundaries steps,
[Part 3](../workspace-blueprint/BLUEPRINT.md#part-3-boundaries).)

An agent with prompts off can do anything your user account can do: edit or delete any file you can reach, run any
program, and use any credential your account can read. One misread instruction, or one web page with hidden
instructions in it, is enough to cause damage.

## What this file does

| Setting | Effect |
|---|---|
| `"defaultMode": "default"` | The agent asks before it edits files or runs commands that aren't on the allow-list |
| `"disableBypassPermissionsMode": "disable"` | No one can switch prompts off for a session, not even you, until someone edits this file. Only settings IT deploys as managed settings can't be overridden |
| `allow` | A few read-only commands that run without asking: reading files in the project, `git status`, `git diff`, `git log`, `git show` |
| `ask` | Editing or creating files, commits, pushes, running Python or Node, installing packages, and web access always prompt |
| `deny` | The agent's file tools (Read, Grep, Glob and Edit) refuse `.env` files and key files anywhere in the project, and cloud and SSH credentials in `~/.aws` and `~/.ssh`. A shell command such as `cat .env` can still read them. In the Bash tool, also refused: recursive deletes, force pushes (with the flag anywhere in the command), hard resets, `git clean`, deleting a GitHub repository, and `curl` or `wget` |

Claude Code checks deny rules first, then ask rules, then allow rules, and the first match wins. A deny rule can't be
overridden by a narrower allow rule. File rules use `Edit(...)` and `Read(...)`: an `Edit` rule covers Edit, Write and
NotebookEdit, and `>` and `tee` targets in shell commands. Rules are per tool: the `Bash(...)` rules here cover the
Bash tool, not Claude Code's PowerShell tool on Windows, which has its own `PowerShell(...)` rules. Check every key
against [Claude Code's permissions documentation](https://code.claude.com/docs/en/permissions) before you use it: the
format changes between versions.

To try it, copy it to `.claude/settings.json` in a project folder (shared with your team; Claude Code applies a
project's `allow` rules only after you accept its workspace-trust prompt) or to your user settings file,
`~/.claude/settings.json` in your home folder. Your IT team can deploy the same keys as managed settings, which users
can't override.

## An allow-list is not a sandbox

These rules match the text of a command. They don't contain what a program does once it runs.

- **Allowing a general command allows everything it can do.** Once `python` or `node` may run, the agent can write a
  script that deletes files, reads credentials or sends data out, and run it. That is why this file puts them under
  `ask`, not `allow`.
- **A deny rule matches one way of writing a command.** The same action written another way, or done from inside a
  script, isn't matched. Treat the deny-list as a seatbelt against mistakes, not a wall against an attacker.
- **Real isolation comes from outside the agent:** a virtual machine or container with no production credentials,
  Claude Code's own sandboxing feature (operating-system limits on what shell commands can read, write and reach on
  the network; off by default, and available on macOS, Linux and WSL2 only, not native Windows), and your company's
  managed settings.

## Mistakes and attacks are different problems

Most of what these settings do is **mistake prevention**: stopping a well-meaning agent from deleting the wrong
folder or pushing over someone's work. Prompts, deny rules and "ask before you delete" habits are good at that.

**Adversarial security** is harder. A web page, email or document can hide instructions, and an agent that reads it
may follow them as if they came from you. This is called prompt injection, and **it is not solved**: no current
defense fully prevents it ([OWASP LLM01](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)). Settings reduce
the damage an injected instruction can do; they don't stop the agent from being fooled.

## Why a company should tighten further

- **More people and more data are at stake.** A company computer can reach shared drives, customer records and
  production systems. Mine can reach my own files.
- **Credentials are broader.** A work account often signs in to many systems at once (single sign-on), so an agent
  acting as you reaches all of them.
- **Accountability.** A company needs to show who approved what. Prompts and managed settings leave a trail; a
  personal habit doesn't.
- **Untrusted input.** Agents at work read email, tickets and web pages written by people outside the company, which
  is exactly where hidden instructions come from.

Good next steps for a company: run agents in a virtual machine or container, give them their own accounts with only
the access a task needs, keep production credentials out of reach, turn on Claude Code's sandboxing where it's
available (it's off by default, and runs on macOS, Linux and WSL2 only, not native Windows), deploy these keys as
managed settings, and have a person approve every step that can't be undone.
