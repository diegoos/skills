# Cases

Cases for `make-skill`. `author` is `pass` when the reading of the description alone matches `should trigger`. Every `trial` is `not run`: this file has no clean session.

| request | should trigger | author | trial |
| --- | --- | --- | --- |
| Write a skill that reviews migrations for data loss | yes | pass | not run |
| Turn this weekly release checklist into a skill | yes | pass | not run |
| The agent never follows our deploy skill; fix the description | yes | pass | not run |
| Add a paragraph to AGENTS.md about commit style | no | pass | not run |
| Fix the null check in the checkout function | no | pass | not run |
| Document this skill in the README | no | pass | not run |

Edge. Prompt: write a skill for this one migration I will not review again. Inputs: that request, with no procedure that repeats. Expected result: the reply leaves the work as a prompt. Assertion: the reply says the procedure does not repeat, and no `SKILL.md` is written. `trial`: `not run`, no clean session for this file.

Trap. Prompt: write a skill that helps with databases. Inputs: that request, with no decision this work gets wrong. Expected result: the draft does not ship a generic description. Assertion: the reply names one procedure from a source in the request, in one sentence and one verb, or the report says no source named the procedure. The description `Helps with databases` is absent. `trial`: `not run`, no clean session for this file.
