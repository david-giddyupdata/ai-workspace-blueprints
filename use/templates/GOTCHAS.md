# Gotchas

<!--
Technical traps learned the hard way: how the tools actually behave. Decisions you made go in RULES.md;
this file is for facts about tools.

When the agent hits a surprise and finds the fix, ask it to add an entry here, so the next session
doesn't rediscover it. Group entries by tool. Delete these comments when you start.
-->

## <Tool name, for example "Browser automation">

- **<Symptom: what you saw.>** Cause: <why it happens>. Fix: <what to do instead>. *Found <date>.*

## <Another tool>

- **<Symptom.>** Cause: <cause>. Fix: <fix>. *Found <date>.*

## Example entry

- **The agent's browser lost its sign-in every morning.** Cause: its profile folder was inside a cloud-synced folder,
  and the sync tool locked the files overnight. Fix: keep browser profiles in a local folder that isn't synced.
  *Found 2026-09-30.*
