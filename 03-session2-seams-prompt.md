# Session 2 prompt: connect Databricks and the config

Do this after session 1 passes. Open the work repository in plan mode and give the agent the prompt below.

```
Read PORTING.md sections 3, 4 and 6:
https://github.com/surahli123/work-prompts/blob/main/PORTING.md
Do not rewrite kangaroo code. Do not write a Databricks client or a new connector.
Use the Databricks MCP server or skill that this laptop already has.
Change only: ~/.kangaroo/overlay/warehouse.json, one small wrapper script if the cmd
route needs it, and CliConfig in kangaroo/sources/config.py with the place where
analyze picks it (kangaroo/api.py).

1. Find the Databricks tools. List the MCP servers and tools that you can call, and the
   skills that query Databricks. For each one: its name, its input, its output, and
   if it can write. Then choose a route:
   - cmd: a skill script or CLI can run one SQL statement and give JSON.
   - handoff: only an MCP tool can run SQL.
   Show the list and your choice. Stop and wait for my approval.
2. Complete ~/.kangaroo/overlay/warehouse.json from ~/ds-handoff/alias_map.md
   (PORTING.md section 3): tables, t3_columns, assignment, split_count_metric, approved,
   cohort. Keep "dialect": "spark". Real names go only into that file.
3. cmd route only: write a wrapper that reads SQL on stdin, runs it with the skill
   script or CLI, and prints the JSON result. The result can be a list of rows or the
   Databricks statement result (manifest and data_array). Test it with: SELECT 1 AS n.
4. Dry run: python3 bin/kangaroo dry-run --out /tmp/kangaroo-dry
   Run each file with your route. Each must compile and return no rows.
   Show the names of the files that fail, with the error.
5. Complete CliConfig with the config CLI code in legacy/. In analyze, use CliConfig
   when no --config and no --configs is given.
6. Contract. Run: python3 bin/kangaroo contract-template --scorecard <export.csv>
   --out /tmp/contract.json. I fill in the primaries, bars and guardrails.
7. Analyze the flight. The scorecard export gives T1; Databricks gives the cuts.
   - cmd:     python3 bin/kangaroo analyze --scorecard <export.csv>
                  --contract /tmp/contract.json --warehouse "cmd:<wrapper>"
   - handoff: python3 bin/kangaroo analyze --scorecard <export.csv>
                  --contract /tmp/contract.json --warehouse handoff:/tmp/kangaroo-q
     For each file in /tmp/kangaroo-q/pending/: run its SQL with the Databricks read
     tool, and save the tool output, without changes, as
     /tmp/kangaroo-q/results/<same name>.json. Do not type, round or change a number:
     each row has a checksum, and a changed result is refused. Run analyze again.
     Repeat until no statement is pending.
8. Checks:
   - python3 -m unittest discover -s tests passes;
   - each cut ran or shows an access gap;
   - trace.json has no rows (only statement IDs, counts and aggregates);
   - python3 bin/kangaroo check-report says 0 problems.
9. Show on screen only counts: tests, dry-run files that compile, cuts that ran,
   access gaps, and the grade of each arm. Use aliases. No metric values, no rows.
Use only read tools. Do not create tables, jobs or files in Databricks.
Commit locally. Do not push.
```
