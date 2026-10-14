# Work prompts

Prompts and instructions for the coding agent on the work laptop. The laptop reads this repository and writes nothing back. The code is in a separate repository: [kangaroo](https://github.com/surahli123/kangaroo), the search experiment agent.

| File | What it is | Status |
|---|---|---|
| [01-materials-prompt.md](01-materials-prompt.md) | Questions about the current work agent. The answers gave the materials for the kangaroo design | Done |
| [PORTING.md](PORTING.md) | How the work agent becomes kangaroo: the session order, the aliases, the four seams, the test rules, what to send home | Current. A copy of the kangaroo file |
| [02-session1-replace-prompt.md](02-session1-replace-prompt.md) | Session 1: list what the work repository has, move it to `legacy/`, copy kangaroo, analyze one real flight | Done |
| [03-session2-seams-prompt.md](03-session2-seams-prompt.md) | Session 2: update kangaroo, connect Databricks through the MCP or skill that the laptop already has, and the config CLI | Done |
| [04-session3-loop-prompt.md](04-session3-loop-prompt.md) | Session 3: fix the no-bar call, confirm past-flight cards, check the tests | Next |

Kangaroo is copied, not rewritten. New code is written only for the work seams. Queries go through the existing Databricks MCP or skill, not a new client. Do one session at a time, in plan mode, and approve each plan before the agent edits. Only counts come home: no metric values, no rows and no names from the alias map.

The laptop must be able to read the kangaroo repository on GitHub.
