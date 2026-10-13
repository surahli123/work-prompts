# Session 2 prompt: connect the work seams

Do this after session 1 passes. Open the work repository in plan mode and give the agent the prompt below.

```
Read PORTING.md sections 3, 4 and 6:
https://github.com/surahli123/work-prompts/blob/main/PORTING.md
Do not rewrite kangaroo code. Change only these:
- overlay/ (new, made from overlay.example/);
- McpWarehouse in kangaroo/sources/warehouse.py, and the "mcp" kind in
  warehouse_from in kangaroo/run.py;
- CliConfig in kangaroo/sources/config.py, and where analyze picks the config source.

1. Make overlay/warehouse.json from overlay.example/ and ~/ds-handoff/alias_map.md
   (PORTING.md section 3). Real names go only into overlay/. Do not commit overlay/
   to a repository that leaves this laptop.
2. Complete McpWarehouse. Use the connection code in legacy/ for the endpoint and its
   authentication. Use only the allow-listed read tool, never the dashboard write tool.
3. Complete CliConfig with the config CLI code in legacy/. In analyze (kangaroo/api.py),
   use CliConfig when no --config and no --configs is given.
4. For each cut template, run cuts.dry_run_sql (Spark, LIMIT 0). If a template does not
   compile, show its name and the error.
5. Run: python3 bin/kangaroo analyze --experiment <one real flight> --warehouse mcp
6. Checks:
   - python3 -m unittest discover -s tests passes;
   - each cut runs or shows an access gap;
   - trace.json has no rows (only statement IDs, counts and aggregates);
   - ste.check finds 0 problems in the report.
7. Show on screen only counts: tests, templates that compile, cuts that ran, access gaps,
   and the grade of each arm. Use aliases. No metric values, no rows.
Commit locally. Do not push.
```
