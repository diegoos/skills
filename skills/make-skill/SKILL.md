---
name: make-skill
description: >-
  Writes or edits an AI agent skill (`SKILL.md`, `references/`). Use when the user wants to create a skill, turn a repeated workflow into a skill, split or tighten a skill, write or fix a skill's description so it triggers, or debug a skill the agent does not follow. Skip when the task is an always-on instruction file or application code.
metadata:
  version: 0.1.0
  author: "Diego Oliveira"
  tags:
    - skills
    - agent-skills
    - prompt-design
---

# Make skill

You write skills that other agents read. A good skill makes each run follow the same process, not the same wording. The request gives the facts. This guide gives the judgment.

Work in this order. Finish a step when its **Done when** holds, then take the next.

1. [Find the repeat](#find-the-repeat).
2. [Choose invocation](#choose-invocation).
3. [Write the description](#write-the-description).
4. [Structure the skill](#structure-the-skill).
5. [Write the steps](#write-the-steps).
6. [Prune](#prune).
7. [Write the cases](#write-the-cases).
8. [Check the draft](#check-the-draft).

A new skill walks all eight. A failed trigger walks Write the description, Write the cases, and Check the draft. A rushed step walks Write the steps, Write the cases, and Check the draft. A tightening walks Prune, Write the cases, and Check the draft. A split walks all eight steps for each resulting skill. On every route, Write the cases decides whether this run writes `cases.md`. The failed-trigger and rushed-step routes open [Iterate](references/evaluation.md#iterate) before the edit.

Read [`references/example.md`](references/example.md) when this is the first skill of the session, or when the draft fails the check.

## Terms

- **Context pointer**: a line the agent always holds that names material outside the context and says when to read it. A skill's description is one.
- **Branch**: a distinct case a skill handles, so different runs take different paths.
- **Leading word**: a short concept the model already knows, used as one token to steer behavior.
- **Completion criterion**: the condition that shows a step is done.
- **Collection**: a set of skills the request names.

[`references/principles.md`](references/principles.md) is the authority for pointers, completion criteria, leading words, negation, pruning, and size.

## Rules for every step

Record a missing detail as an assumption and keep drafting. Ask only when the answer changes the outcome and no safe default exists. Name a check you cannot run, and finish the rest. The reply says what a step needs said, in the agent's own shape. Creating and editing files inside the skill folder can proceed. Deleting a skill folder, publishing, or sending waits for approval of that action. The user's instructions come first, then the host or team rules, then this guide.

## Find the repeat

A skill earns its place when a procedure repeats. When the request is a one-off, say so and leave it as a prompt.

Take the procedure from the first source that answers, in order: the request, the work (a runbook, a spec, review comments, a resolved failure, or a correction the user keeps giving), a place the request named, then one question. Leave out a branch no source named. Generic best practice names no decision this work gets wrong.

Put a fact that every run needs in the always-on instructions of the place where the agent works. A skill loads only when it fires.

Carry a repository, path, or file only when the request names that context, and mark it as that context's fact.

When a named source is missing, write the steps the request covers, mark the steps that depend on the source, and report the gap.

Give the skill one job, in one sentence, around one verb. Move a second job into its own skill when one description would trigger on the wrong job, and leave the jobs together when the split would make the skills fight.

Mark a workaround for a current model limit as a capability, and review it when the model changes. Mark a process or domain rule as a preference.

Read [What earns a skill](references/principles.md#what-earns-a-skill) when the request could be a prompt, always-on instructions, or a skill.

**Done when:** one sentence names the procedure around one verb, or on an edit names the procedure the skill already repeats. The run treats the request as a skill, a prompt, or an always-on instruction. When it is a prompt or an always-on instruction, the reply says so and no skill file is written.

## Choose invocation

Choose model invocation when the agent must reach the skill on its own. The description stays in context on every turn. Choose user invocation when only a person starts it, and set `disable-model-invocation: true` where the client supports it. The person then carries the index, and the description costs nothing. The two budgets are under [Two budgets](references/principles.md#two-budgets).

Read [Invocation and the human index](references/principles.md#invocation-and-the-human-index) when many user-invoked skills need a router, or when skills share reference material. Read [`references/example-router.md`](references/example-router.md) when the choice is user invocation, a router, or a shared reference. Put that choice in the skill.

**Done when:** the mode matches who must reach the skill, and a router or a shared reference is named when the skill needs one.

## Write the description

The description is the top-level context pointer. The agent reads it on every turn and uses it to decide whether the skill applies. Model invocation uses the list below. User invocation is one line and has no trigger list.

- Start with the verb that names the job, then the main trigger. Some clients truncate long descriptions, and the start survives.
- A branch is one path. Put every wording of that path in the same Use when clause. Keep a wording when cutting it would miss a real request, and cut a wording that only repeats one you kept. The test is under [Pointers](references/principles.md#pointers).
- Use the words a user types, including casual forms, abbreviations, and requests that leave the domain unnamed.
- Add a skip clause when a nearby task could match by mistake. When the request names a collection, read the sibling descriptions, and give a skip clause on both sides when one job neighbors the other.
- Write in the third person, with a "Use when…" clause.
- Leave out identity the body already states.
- Keep it under 1,024 characters, in a few sentences, with no markup tags.

Weak: "Helps with skills."

Strong: "Reviews a migration for data loss. Use when the user asks to check a migration. Skip when the task is to write a schema."

**Done when:** a model-invoked description states each branch once, includes a "Use when…" clause, includes a skip clause when a nearby task could match, stays under 1,024 characters, and starts with the job, then the main trigger. A user-invoked description is one line and has no trigger list.

## Structure the skill

A new skill is `SKILL.md` with the quality floor: one verb, a description that can trigger, and a checkable criterion on each step. Keep `SKILL.md` under about 500 lines. Add `references/` when a branch needs text the other steps do not use. Add `scripts/` when a step must be exact. Add `cases.md` when the user asks for cases, tests, or validation. Those files combine in any set. Read [Size to the work](references/principles.md#size-to-the-work) before you add or remove a file. Copy [`assets/SKILL.template.md`](assets/SKILL.template.md) for the `SKILL.md` core. The reasons for a pointer are under [Pointers](references/principles.md#pointers), [Information hierarchy](references/principles.md#information-hierarchy), and [Co-location and sprawl](references/principles.md#co-location-and-sprawl).

- Read [`references/mechanics.md`](references/mechanics.md) before the name, the frontmatter, and the paths.
- Read [Copy when the step needs it](references/mechanics.md#copy-when-the-step-needs-it) when a step uses an input, the caller checks a shape, a nearby task could match, or a required input can be missing.
- Read [Security and state changes](references/mechanics.md#security-and-state-changes) before a step deletes, publishes, or sends.
- Read [Scripts](references/mechanics.md#scripts) when a step must be exact.
- Read a local convention only when the request names a collection or a client.

**Done when:** a new skill's files are the ones this step adds, an existing skill's files match [Size to the work](references/principles.md#size-to-the-work), and `SKILL.md` stays under about 500 lines.

## Write the steps

End every step on a criterion the agent can check, and write the demand into it so the step forces the full work. When a step rushes, sharpen the criterion before you split the sequence. Write the step as an action, give each branch its own route, and make a failed check name the step to redo. Criteria, demand, and splits are under [Completion criteria](references/principles.md#completion-criteria) and [Splitting](references/principles.md#splitting).

### Words

- Give the reason when the rule is not obvious. Leading words and negation are under [Leading words](references/principles.md#leading-words) and [Negation](references/principles.md#negation).
- Use a principle for open work, a template with parameters for variable work, and exact steps or a script for fragile work.
- Give one default path, and offer another path only with a clear trigger.

### Failure

- Every path ends as a result, a named assumption, or a blocked report that names the next action.
- When a step can lose an input, a tool, or a service, add a guard (a fallback, a retry bound, or a blocked exit) and name where the value comes from. The retry counts are in [Failure handling](references/mechanics.md#failure-handling).
- A subagent or a fresh session is a helper. The step still finishes when the helper is absent.

**Done when:** every step has a checkable criterion that forces the full work, states the behavior to perform, and ends in a result, a named assumption, or a blocked report. A guard appears on each step that can lose an input, a tool, or a service.

## Prune

Delete a sentence that would leave the agent's decision unchanged, and keep each meaning in one place. Keep each fact that makes the step apply to the right case. Leave a lookup the agent can run to the environment. Keep a version, a date, or a price in a dated section, or leave it out of the body. The tests are under [Pruning](references/principles.md#pruning).

**Done when:** every remaining sentence would change a decision, none repeats a lookup the agent can run, and each fact that makes the step apply to the right case stays.

## Write the cases

`cases.md` appears when the user asks for cases, tests, or validation, or when the folder already has the file. When the folder already has it, update the cases the change can break. When a wrong result does not show in the criterion and reading the draft is not enough, suggest the file once, in one sentence, and continue the route. When the run writes the file, the records come from [Cases file](references/evaluation.md#cases-file), and this skill's `cases.md` stays in this folder. The three-run trial and turning feedback into cases open when `cases.md` is part of this run, in [`references/evaluation.md`](references/evaluation.md). The 10–20 suite opens when a clean-session trigger trial is `fail`, and then those requests are the trigger records. An `author` miss is fixed in the description. Without the file, the failure stays in the reply.

**Done when:** `cases.md` is in the folder only because the user asked or the folder already had it, and a file this run writes matches [Cases file](references/evaluation.md#cases-file).

## Check the draft

This gate judges. Whole-draft checks and trials are in [`references/evaluation.md`](references/evaluation.md). Answer every question. A no on a step this route walks sends that step back. A no on a step this route skips stays in the reply. A `not run` leaves the step in place. When the next pass returns the same no, record it and finish.

- Does the description match the invocation: third person, a "Use when…" clause, under 1,024 characters, and the job verb first, then the main trigger, when the agent chooses the skill; a skip clause when a nearby task could match; and a one-line summary with no trigger list when only a person starts it?
- Can the agent tell, from each criterion alone, when the step is done, and does the demand force the full work?
- When the folder has `references/`, does each pointer name its file and its condition, and does every branch with depth sit behind one? When the folder has no `references/`, the check is `not run`.
- When a step uses an input, does the skill name it? When the caller checks a shape, does the skill name the output? When a required input can be missing, does the skill name the blocked exit? When none of these hold, the check is `not run`.
- When a step can lose an input, a tool, or a service, does that step have a fallback, a retry bound, or a blocked exit? When no step can lose one, the check is `not run`.
- Would every line change a decision, and does each fact that makes a step apply to the right case remain?
- Does the skill stay general unless the request named a context?
- When this run writes `cases.md`, or the folder already has it, does the file match [Cases file](references/evaluation.md#cases-file)? When the file is absent, the check is `not run`.
- Has a clean-session trial run when `cases.md` is part of this run, or when the description shares words with a neighbor skill? When that required trial did not run, the reply says the trigger was not checked. When the trial is not required, the reply leaves that unsaid. A trigger was checked only when that session ran it. The load check is the Baseline bullet in [`references/evaluation.md`](references/evaluation.md).
- For a change that claims a gain, is the evidence in [Claimed gains](references/evaluation.md#claimed-gains) present, or does the reply say the gain was not measured?
- Does `SKILL.md` stay under about 500 lines?
- Do the frontmatter and the paths follow [`references/mechanics.md`](references/mechanics.md)? Each `path#anchor` file exists, each anchor matches a heading, and `name` matches the folder.

The reply names the files written, any check that did not run, any assumption, where the skill was placed, and a gain when one is claimed. Read [`references/evaluation.md`](references/evaluation.md) when you tune a description, when the one trial fails, or when a failure needs a classified fix.

**Done when:** each question has an answer, every no is in the reply, no skipped step was rewritten, the same no did not start another pass, and a claimed gain meets [Claimed gains](references/evaluation.md#claimed-gains) or the reply says the gain was not measured.
