# Evaluation and iteration

Reference for [`SKILL.md`](../SKILL.md). The gate in that file judges the draft. This file holds whole-draft checks and trials. When a trial cannot run, say so, with the reason. A check for a file this run does not have is `not run`.

## Cases file

Read this when the run writes `cases.md`.
The file sits beside `SKILL.md` as an input.

Write three requests that should trigger, three that share words and ask for another job, and two functional cases, one edge and one trap.
When the request names a collection, one of those near-miss requests is a sibling skill's trigger.
Judge a trigger request from the description alone.

A trigger record is `request | should trigger | author | trial`.
A functional record is `prompt | inputs | expected result | assertion | trial`.
`author` is `pass` when the reading of the description matches `should trigger`.
`author` is `fail` when that reading and `should trigger` differ.
`trial` is `pass`, `fail`, or `not run`, and only a clean session fills `pass` or `fail`.
A trial that did not run stays `not run`.
When the 10–20 suite runs, those requests are the trigger records in the file.

## Check by reading

Open the dry run and the fresh reader on the trigger route, when the one trial fails, or when a failure needs a classified fix. The trigger suite opens when a clean-session trigger trial is `fail`. An `author` miss is fixed in the description and does not open the suite.

- **Triggers.** Write 10 to 20 realistic requests. Half should trigger the skill, and half should not. Include near-misses: requests that share words with the skill but need a different job. Vary the form (formal, casual, typos), the explicitness (named domain or not), and the complexity (one step or several). Decide from the `description` alone whether each request triggers. Record `author` and `trial`, as in [Cases file](#cases-file).
- **Dry run.** Pick one realistic case and walk the draft's steps in order. Write the input, the action, and the output of each step. Mark each step that can lose an input, a tool, or a service, and confirm that it has a fallback, a retry bound, or a blocked exit.
- **Fresh reader.** If a second agent with a clean context is available and `cases.md` exists, have it run the cases and report what was unclear. If that agent is absent, or the file is absent, re-read the skill as a reader who has never seen it.

## Check with trials

Trigger trials and functional cases open when `cases.md` is part of this run.

- **Trigger trials.** Run each request three times from a clean context. A request that should trigger passes when it triggers in more than half of the runs. A request that should not trigger passes when it triggers in fewer than half. When the trigger records are the 10–20 suite, keep a holdout of requests, and tune the description only on the other requests. When the records are the set in [Cases file](#cases-file), run every request. A simple one-step task may not trigger even with a correct description. Judge the description on the multi-step requests too.
- **Functional cases.** Start with the edge and the trap in [Cases file](#cases-file), and add one whenever a failure appears. Each case has a realistic prompt, its input files, and the expected result.
- **Baseline.** A clean-session trial runs when `cases.md` is part of this run, or when the description shares words with a neighbor skill: one creation or edit trial from a clean context on the smallest model you can run. Where possible, also run each case with and without the skill, each time from a clean context. When you change a skill, compare it with a snapshot of the previous version. When that trial is required, check the load with the client's list command when it has one, otherwise with the documented discovery path. When the required trial or its load check did not run, the reply says the trigger was not checked. When the trial is not required, the reply leaves that unsaid. When the load stayed unchecked, the reply says so.
- **Assertions.** Write each assertion so the output can confirm it. "Good output" is too vague. An exact string match is too brittle. A pass needs evidence in the output. Compare the output to the assertion. Add assertions after the first run, when real outputs exist.
- **Reviewers.** Judge style and overall quality with a reviewer, human or model, or with a blind comparison of two versions.
- **Traces.** Read the execution trace, not only the final answer. Look for wasted steps, steps done out of order, reference files that never open, and files that open on every run.
- **Measures.** Track three things: correctness, compliance with the required tools and format, and cost in tokens and time. Count with a tokenizer when one is available; otherwise use the count command the environment has, the same command on both sides, and name the command in the report.

## Claimed gains

A gain is claimed only when the reply says the change makes the skill smaller, faster, or more reliable than the previous one. A wording change that does not say that leaves the gain unclaimed.

- A new skill has no previous text, so there is no delta. The trial and the load check follow the Baseline bullet in [Check with trials](#check-with-trials).
- More reliable, including a one-job skill: the trial result is enough.
- Smaller or faster: the token delta of `SKILL.md`, with the description counted apart, plus one trial. Without the delta, the reply says the gain was not measured.
- No measure, or a trial you cannot run: the reply says the gain was not measured, and why.
- No claim of smaller, faster, or more reliable: the reply leaves the gain unclaimed.

## Iterate

- **Classify each failure before you edit.** A trigger failure (no trigger, or a trigger on a neighbor) changes the description's triggers or skip clause, or the wording of a pointer that should have fired. Cut in this order: a sentence the body already states, a wording that only repeats one you kept, then a later trigger before you cut the first sentence. Sharpen the wording before you move material inline. A method failure (wrong or skipped steps) sharpens a criterion, moves a buried step up, or splits a rushed sequence. In a trace, a step that ends before its criterion is met is a criterion defect. An output failure (wrong format or content) tightens the template, adds an example, or moves rigid formatting into a script.
- **Generalize.** The fix uses the branch's words. Words copied from the failing request serve only that request.
- **Review the passes too.** Ask which triggers were false positives, what was missing, and what can be cut. Simplify before you add: when a check fails, try removing or shortening an instruction before you add a rule.
- **Turn feedback into cases.** When `cases.md` is part of this run, collect feedback from real use, turn each failure into a case, and rerun the whole set after each change.
- **Choose the best version by the checks.** The best version passes the most checks. It is not always the last one.
- **Stop when the work stops improving.** Stop when the planned checks pass, when a round brings no new evidence, or when the remaining gaps are written in the report. If nothing improves, check the checks before you edit the skill again.
- **Restructure when a description stays weak.** After several rounds, change its structure (branches, order, leading word), not only its words.

## Lifecycle

- Run the checks again when the model, a tool, or a script changes. Retire a capability rule when the model handles the task without it.
- Review skill changes like code changes. Keep the previous version so you can roll back. When `cases.md` exists, run every case before you promote a version. When an edit claims a gain, the previous text has to stay reachable. Without that text, the reply says the gain was not measured.
- When `cases.md` exists, remove a rule that no case needs. If something still depends on it, move it to a section marked legacy.
