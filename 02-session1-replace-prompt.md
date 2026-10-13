# Session 1 prompt: replace the work agent with kangaroo

For the coding agent on the work laptop (Codex, Cursor or Claude Code). Open the repository of the current work agent in plan mode. Give the agent the prompt below, as written.

```
Read these files first (if a link does not open, clone the repository and read the file):
- PORTING.md: https://github.com/surahli123/work-prompts/blob/main/PORTING.md
- AGENTS.md:  https://github.com/surahli123/kangaroo/blob/main/AGENTS.md
The kangaroo repository (https://github.com/surahli123/kangaroo) replaces this agent.
Do not rewrite kangaroo code. Copy it. Write new code only for the seams in PORTING.md.
If a document here disagrees with PORTING.md, PORTING.md wins. List each disagreement.
Do not run data queries in this session.

1. Inventory. List what this repository has that kangaroo does not: modules, specs,
   skills, data files, traces, knowledge files, tests. For each, write one of:
   "move to legacy/", "keep as a seam" (warehouse connection, config CLI, alias map),
   or "needs a decision". Show the list and stop. Wait for my approval.
2. After my approval:
   - git mv all current code and docs into legacy/. Do not delete anything.
   - git clone --depth 1 https://github.com/surahli123/kangaroo into a temporary folder.
     Copy everything except .git into this repository, without changes.
3. Run: python3 -m unittest discover -s tests
   Run: python3 -m kangaroo demo --out /tmp/kangaroo-demo
   Both must pass. If one fails, stop and show the name and message of the failure.
4. Make sure that no code outside legacy/ imports legacy/.
5. I will give you the scorecard of one real flight as a CSV: the T1 rows of its
   latest snapshot.
   Run: python3 bin/kangaroo init
   In ~/.kangaroo/overlay/warehouse.json, set "t1_columns" so that each kangaroo name
   maps to its CSV column, with "_percent_fields" if the relative fields are percents
   (PORTING.md section 3, the alias map). Real names go only into that file.
   Run: python3 bin/kangaroo analyze --scorecard <that file>
   If it names a missing column, fix "t1_columns" and run it again.
6. Show on screen only:
   - the test and demo results;
   - for the real flight: the grade of each arm, the launch call, and the number of
     open questions, cuts and access gaps.
   Use aliases from ~/ds-handoff/alias_map.md for every real name.
   Show no metric values and no rows.
Commit locally. Do not push.
```

The flight gets M1 output from the scorecard alone. The deep-dive cuts show as access gaps until session 2 connects the warehouse.
