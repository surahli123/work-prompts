# Session 3 prompt: the learning loop and the tests

Do this after session 2 passes: the session 2 handoff note is written, and a cut agrees with T1 (each arm's delta). Open the work repository in plan mode and give the agent the prompt below.

```
Read PORTING.md sections 4, 7 and 8, the session 2 handoff note, and ~/ds-handoff/upstream.md:
https://github.com/surahli123/work-prompts/blob/main/PORTING.md
The rules of sessions 1 and 2 still apply: read tools only; tables only from "approved";
flights only from the approved flight scope; aliases on screen; no metric values, no rows.
A change to kangaroo code needs my approval for that change, a test, and an entry in
upstream.md. Do not turn the sandbox off.

0. Before you start:
   - If kangaroo on GitHub has commits after the one you last merged, take them with
     git apply -3, as in session 2 step 0. Run the tests.
   - Propose a fix: when a primary has no bar, the call must be "Not made", not Ship.
     After my approval, add a test that fails without the fix, and an upstream.md entry.
   Show the results. Stop and wait for my approval.
1. Flights. List the finished flights in the approved flight scope, with aliases. I
   choose which become cards and which one is the similar flight. A card is never
   similar to itself, so the similar flight must be a different flight.
2. Cards. Analyze each card flight from live T1, the same way as the session 2 flight:
   handoff route, CliConfig (I run the config CLI if the sandbox blocks it), a draft
   contract for each. Then ask me for the cause and the lesson of each flight. Record:
   python3 bin/kangaroo cards confirm EXPERIMENT --cause "..." --lesson "..." --approver NAME
   Use only my words and my name. Do not write a cause or a lesson yourself.
3. Analyze the similar flight the same way. Its report must cite one confirmed card.
   If it cites none, show the layer, tags and families of the card and of the flight,
   with aliases, and stop.
4. Tests.
   - In legacy/, list the tests that test legacy code or pin internal state. Do not
     move, copy or delete them.
   - Check each test that you added since session 1 against PORTING.md section 7.
     List any that pins internal state or asserts on prose. Fix only after my approval.
   - Run python3 -m unittest discover -s tests. It must pass.
5. Show on screen only counts: flights analyzed, cards confirmed, the report that cites
   a card (yes or no), cuts that ran and access gaps for each flight, the grade of each
   arm, tests that pass, and upstream.md entries. Use aliases. No metric values, no rows.
Commit locally. Do not push.
```

If the flight scope allows only three flights, confirm two cards and use the third flight as the similar flight. That meets the session check: a report cites a confirmed card. Add more cards when the scope is wider.

Send home the step 5 counts and the entries in `~/ds-handoff/upstream.md`, with no real names, IDs or values. Kangaroo takes the local changes back from those entries.
