# Security

## Reporting a problem

If you find something here that shouldn't be public (a key, a password, an email address, an account number, a
private name), or an instruction that could make an agent do something unsafe, please report it privately: open this
repository's **Security** tab and choose **Report a vulnerability**, or use the contact form at
https://giddyupdata.com/contact.html. Please don't open a public issue for these.

I'm one person. I aim to reply within a week; when I'm teaching or traveling it can take longer. There is no bug
bounty.

## In scope

- Secrets or personal details committed by mistake, anywhere in the repository.
- Anything in `START_HERE.md`, `AGENTS.md` or `use/` that could lead an agent to damage files, accounts or money in a
  way the documentation doesn't warn about.

## Out of scope

- The two worked examples live in their own repositories; report problems there.
- Vulnerabilities in third-party tools. Please report those to their maintainers.

## If you use these files

- Never put keys or passwords in a file or a chat. Keep them in a password manager, your operating system's keyring
  or a secrets manager.
- Keep the permission prompts on. On my own computer I run with them off and rely on habits instead; that describes
  my setup, it isn't a recommendation. At work, follow your company's rules. At a company, start from `use/settings/`
  and talk to your IT or security team.
- Prompt injection (hidden instructions in a page, email or document) is not solved. Keep agents away from data and
  actions they don't need.
