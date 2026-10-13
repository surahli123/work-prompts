# Session 2 prompt: connect Databricks and the config

Do this after session 1 passes. Open the work repository in plan mode and give the agent the prompt below.

```
Read PORTING.md sections 3, 4 and 6, and the session 1 handoff note:
https://github.com/surahli123/work-prompts/blob/main/PORTING.md
Do not rewrite kangaroo code. Do not write a Databricks client or a new connector.
Use the Databricks MCP server or skill that this laptop already has.
Change only: ~/.kangaroo/overlay/warehouse.json, one small wrapper script if the cmd
route needs it, and CliConfig in kangaroo/sources/config.py with the place where
analyze picks it (kangaroo/api.py). Any other change to kangaroo code needs my approval
for that change, a test, and an entry in ~/ds-handoff/upstream.md (PORTING.md section 8).

0. Update kangaroo and record the local changes.
   - git clone https://github.com/surahli123/kangaroo into a temporary folder, with history.
   - Make the diff from the kangaroo commit that session 1 copied to the latest commit.
     Apply it here with git apply -3. Keep the local commits. Resolve each conflict.
   - Run: python3 -m unittest discover -s tests
   - Make ~/ds-handoff/upstream.md if it does not exist, in the format of PORTING.md
     section 8. Write one entry for each local change to kangaroo code since the copy,
     with the changes from session 1. No real names, IDs or values.
   Show the conflicts, the test result and the entries. Stop and wait for my approval.
1. Find the Databricks tools. List the MCP servers and tools that you can call, and the
   skills that query Databricks. For each one: its name, its input, its output, and
   if it can write. Then choose a route:
   - cmd: a skill script or CLI can run one SQL statement and give JSON.
   - handoff: only an MCP tool can run SQL.
   Show the list and your choice. Stop and wait for my approval.
2. Complete ~/.kangaroo/overlay/warehouse.json from ~/ds-handoff/alias_map.md
   (PORTING.md section 3): tables, t1_columns, t3_columns, assignment,
   split_count_metric, cohort, prefer_cuped, prefer_sequential.
   - If T1 does not have a kangaroo column, map it to a SQL expression: a struct field,
     an array element, or NULL. Do not change kangaroo/sources/t1.py for this.
   - If a cut template uses a value that T3 does not have, map it in "t3_values". If T3
     does not have a column, map it to null in "t3_columns". Do not edit a template.
   - Set "multi_arm" in "assignment" to the rule that makes a cut agree with T1.
   - Do not change "approved". I add a table to it only after the privacy decision.
   - Keep "dialect": "spark". Real names go only into that file.
3. cmd route only: write a wrapper that reads SQL on stdin, runs it with the skill
   script or CLI, and prints the JSON result. The result can be a list of rows or the
   Databricks statement result (manifest and data_array). Test it with: SELECT 1 AS n.
4. Complete CliConfig with the config CLI code in legacy/. In analyze, use CliConfig
   when no --config and no --configs is given. If the CLI runs only outside the
   sandbox, I run it and give you the JSON with --config.
5. Analyze the session 1 flight from live T1, with the draft contract:
   - cmd:     python3 bin/kangaroo analyze --experiment <name or config id>
                  --contract <draft contract> --warehouse "cmd:<wrapper>"
   - handoff: python3 bin/kangaroo analyze --experiment <name or config id>
                  --contract <draft contract> --warehouse handoff:/tmp/kangaroo-q
     For each file in /tmp/kangaroo-q/pending/: run its SQL with the Databricks read
     tool, and save the tool output, without changes, as
     /tmp/kangaroo-q/results/<same name>.json. Do not type, round or change a number.
     Run analyze again. Repeat until no statement is pending.
   The cuts on tables that are not approved show as access gaps. That is correct.
6. Compare live T1 with the session 1 run from the console export. Write a temporary
   script that reads the two case/scorecard.json files. For each arm and metric, it
   compares rel_delta and the CI. It prints only counts: agree, differ, in one run only.
   Do not commit the script. If more than a few differ, stop and tell me.
7. Dry run, only after I approve t3 and assignment:
   python3 bin/kangaroo dry-run --out /tmp/kangaroo-dry
   Run each file with your route. Each must compile and return no rows.
   Show the names of the files that fail, with the error. Before the approval, skip
   this step and say so.
8. Checks:
   - python3 -m unittest discover -s tests passes;
   - each cut ran or shows an access gap;
   - trace.json has no rows (only statement IDs, counts and aggregates);
   - python3 bin/kangaroo check-report says 0 problems.
9. Show on screen only counts and names of checks: tests, the route, T1 statements
   that ran, the step 6 counts, cuts that ran, access gaps, dry-run files that compile
   (or "skipped"), the grade of each arm, and the checks that did not pass.
   Use aliases. No metric values, no rows.
Use only read tools. Do not create tables, jobs or files in Databricks.
Commit locally. Do not push.
```

Send home the step 9 counts and the entries in `~/ds-handoff/upstream.md`. Kangaroo takes the local changes back from those entries, so that the next update has no conflicts.
