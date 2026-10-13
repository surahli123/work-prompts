# Phase 0 prompt: audit the work agent

For the coding agent on the work laptop (Codex, Cursor or Claude Code). Open the repository of the current work agent, then give the agent the prompt in the code block below, as written. Use plan mode if the tool has it.

This is phase 0 of `PORTING.md`. It changes no code.

```
Read-only task. Do not edit, commit, push or send anything. Do not run data queries.

Read these two files first:
- PORTING.md: https://github.com/surahli123/work-prompts/blob/main/PORTING.md
- AGENTS.md:  https://github.com/surahli123/kangaroo/blob/main/AGENTS.md
The kangaroo repository (https://github.com/surahli123/kangaroo) is the reference.
If a document in this repository disagrees with PORTING.md, PORTING.md wins.

In this repository:
1. Run the tests. Give the pass and fail counts.
2. List, with file:line:
   - the five state families (sealed, packet, checkpoint, accepted, receipt flags);
   - each place where an M0 result stops M1 or marks it "not ready";
   - the test that pins flags to false;
   - each reference to the retired first-exposure table;
   - the code that calls the warehouse MCP and the config CLI.
3. Make a table: each module here -> the kangaroo module that replaces it,
   or "keep as a seam" (warehouse connection, config CLI, alias map).
4. Write PLAN.md in this repository (do not commit it): phases 1 to 5 of
   PORTING.md. For each phase, give the files it changes and the check
   that proves it is done.
5. List each disagreement between the documents here and PORTING.md.

On screen, show only counts, file paths and the PLAN.md phase list.
Use aliases from ~/ds-handoff/alias_map.md for every real name.
Show no metric values and no rows.
```

When the plan is correct, start phase 1 in a new session.
