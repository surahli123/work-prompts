# Session 3 prompt: the learning loop and the tests

Do this after session 2 passes. Open the work repository in plan mode and give the agent the prompt below.

```
Read PORTING.md sections 4 and 7:
https://github.com/surahli123/work-prompts/blob/main/PORTING.md

1. Cards. For 3 to 5 past flights, analyze each one. Then ask me for the cause and the
   lesson of each flight. Record each one with:
   python3 bin/kangaroo cards confirm EXPERIMENT --cause "..." --lesson "..." --approver NAME
   Use only the words that I give. Do not write a cause or a lesson yourself.
2. Analyze a flight that is similar to one card. The report must cite that card.
3. Tests. In legacy/, list the tests that test legacy code or pin internal state
   (for example the test that pins flags to false). Follow PORTING.md section 7.
   Do not move them out of legacy/. Do not copy them into tests/.
4. Run python3 -m unittest discover -s tests. It must pass.
5. Show on screen only counts: cards confirmed, the report that cites a card (yes or no),
   tests that pass. Use aliases. No metric values, no rows.
Commit locally. Do not push.
```
