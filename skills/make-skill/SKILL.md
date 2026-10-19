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

A new skill walks all eight. A failed trigger walks Write the description, Write the cases, and Check the draft. A rushed step walks Write the steps, Write the cases, and Check the draft. A tightening walks Prune, Write the cases, and Check the draft. A split walks all eight steps for each resulting skill. The failed-trigger and rushed-step routes open [Iterate](references/evaluation.md#iterate) before the edit.

Read [`references/example.md`](references/example.md) when this is the first skill of the session, or when the draft fails the check.

## Terms

- **Context pointer**: a line the agent always holds that names material outside the context and says when to read it. A skill's description is one.
- **Branch**: a distinct case a skill handles, so different runs take different paths.
- **Leading word**: a short concept the model already knows, used as one token to steer behavior.
- **Completion criterion**: the condition that shows a step is done.
- **Collection**: a set of skills the request names.

[`references/principles.md`](references/principles.md) is the authority for pointers, completion criteria, leading words, negation, and pruning.

## Rules for every step

Record a missing detail as an assumption and keep drafting. Ask only when the answer changes the outcome and no safe default exists. List a check you cannot run as not run, and finish the rest. Creating and editing files inside the skill folder can proceed. Deleting a skill folder, publishing, or sending waits for approval of that action. The user's instructions come first, then the host or team rules, then this guide.

## Find the repeat

A skill earns its place when a procedure repeats. When the request is a one-off, say so and leave it as a prompt.

Take the procedure from the first source that answers, in order: the request, the work (a runbook, a spec, review comments, a resolved failure, or a correction the user keeps giving), a place the request named, then one question. Leave out a branch no source named. Generic best practice names no decision this work gets wrong.

Put a fact that every run needs in the always-on instructions of the place where the agent works. A skill loads only when it fires.

Carry a repository, path, or file only when the request names that context, and mark it as that context's fact.

When a named source is missing, write the steps the request covers, mark the steps that depend on the source, and report the gap.

Give the skill one job, in one sentence, around one verb. Move a second job into its own skill when one description would trigger on the wrong job, and leave the jobs together when the split would make the skills fight.

Mark a workaround for a current model limit as a capability, and review it when the model changes. Mark a process or domain rule as a preference.

Read [What earns a skill](references/principles.md#what-earns-a-skill) when the request could be a prompt, always-on instructions, or a skill.

**Done when:** one sentence names the procedure around one verb, or on an edit names the procedure the skill already repeats, and the reply classifies the request as a skill, a prompt, or an always-on instruction.

## Choose invocation

Choose model invocation when the agent must reach the skill on its own. The description stays in context on every turn. Choose user invocation when only a person starts it, and set `disable-model-invocation: true` where the client supports it. The person then carries the index, and the description costs nothing. The two budgets are under [Two budgets](references/principles.md#two-budgets).

Read [Invocation and the human index](references/principles.md#invocation-and-the-human-index) when many user-invoked skills need a router, or when skills share reference material. Read [`references/example-router.md`](references/example-router.md) when the choice is user invocation, a router, or a shared reference. State that choice in the skill and in the report.

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

Keep what every branch needs in `SKILL.md`. Put a branch's depth behind a pointer that names the file and when to read it, and sharpen that wording before you move the material inline. Keep references one level below `SKILL.md`, keep one concept under one heading, and keep `SKILL.md` under about 500 lines. When a reference still never opens, remove the file.

The reasons are under [Pointers](references/principles.md#pointers), [Information hierarchy](references/principles.md#information-hierarchy), and [Co-location and sprawl](references/principles.md#co-location-and-sprawl). Copy [`assets/SKILL.template.md`](assets/SKILL.template.md) when you start a file.

- Read [`references/mechanics.md`](references/mechanics.md) before the name, the frontmatter, and the paths.
- Read [Inputs and outputs](references/mechanics.md#inputs-and-outputs) when you declare what the skill receives and returns.
- Read [Security and state changes](references/mechanics.md#security-and-state-changes) before a step deletes, publishes, or sends.
- Read [Scripts](references/mechanics.md#scripts) when the work must be exact.
- Read a local convention only when the request names a collection or a client.

**Done when:** what every branch needs stays in `SKILL.md`. Each branch with depth has a pointer that names its file and its condition. A skill with no such branch has no pointer.

## Write the steps

End every step on a criterion the agent can check, and write the demand into it so the step forces the full work. When a step rushes, sharpen the criterion before you split the sequence. Write the step as an action, give each branch its own route, and make a failed check name the step to redo. Criteria, demand, and splits are under [Completion criteria](references/principles.md#completion-criteria) and [Splitting](references/principles.md#splitting).

### Words

- Give the reason when the rule is not obvious. Leading words and negation are under [Leading words](references/principles.md#leading-words) and [Negation](references/principles.md#negation).
- Use a principle for open work, a template with parameters for variable work, and exact steps or a script for fragile work.
- Give one default path, and offer another path only with a clear trigger.

### Failure

- Every path ends as a result, a named assumption, or a blocked report that names the next action.
- Name each tool, package, credential, and file a step needs, where the value comes from, and the fallback when it is missing.
- When a step calls a service or the network, bound every retry, then report. Those counts are in [Failure handling](references/mechanics.md#failure-handling).
- A subagent or a fresh session is a helper. The step still finishes when the helper is absent.

**Done when:** every step has a checkable criterion that forces the full work, states the behavior to perform, and ends in a result, a named assumption, or a blocked report.

## Prune

Delete a sentence that would leave the agent's decision unchanged, and keep each meaning in one place. Keep each fact that makes the step apply to the right case. Leave a lookup the agent can run to the environment. Keep a version, a date, or a price in a dated section, or leave it out of the body. The tests are under [Pruning](references/principles.md#pruning).

**Done when:** every remaining sentence would change a decision, none repeats a lookup the agent can run, and each fact that makes the step apply to the right case stays.

## Write the cases

For a new skill, or when the description changed, write three requests that should trigger, three that share words and ask for another job, and two functional cases, one edge and one trap. When the request names a collection, one of those near-miss requests is a sibling skill's trigger. Judge a trigger request from the description alone. Record `request | should trigger | author | trial`, and for a functional case `prompt | inputs | expected result | assertion | trial`. `author` is `pass` when that reading matches `should trigger`, and `fail` when it does not. `trial` is `pass`, `fail`, or `not run`, and only a clean session fills `pass` or `fail`. An edit that leaves the description unchanged keeps the cases the change can break. Keep the cases in `cases.md` beside `SKILL.md`, as an input rather than a reference, and name that file in the report. The 10–20 suite and the three-run trial are in [`references/evaluation.md`](references/evaluation.md), and they open on the trigger route.

**Done when:** the set matches the route, each record has those fields, `author` comes from the description alone, `trial` is `not run` unless a clean session filled it, and the report names `cases.md`.

## Check the draft

This gate judges. Whole-draft checks and trials are in [`references/evaluation.md`](references/evaluation.md). Answer every question. A no on a step this route walks sends that step back. A no on a step this route skips stays in the report. When the next pass returns the same no, record it and finish.

- Does the description match the invocation: triggers when the agent chooses the skill, a skip clause when a nearby task could match, and a one-line summary when only a person starts it?
- Can the agent tell, from each criterion alone, when the step is done, and does the demand force the full work?
- Does each pointer name its file and its condition? Does every branch with depth sit behind one, and does a skill with no such branch have no pointer?
- Does the skill name its inputs, its output, and the blocked exit for a missing required input?
- Does every dependency have a fallback or a named exit?
- Would every line change a decision, and does each fact that makes a step apply to the right case remain?
- Does the skill stay general unless the request named a context?
- Do the cases from [Write the cases](#write-the-cases) match the route?
- For a new skill, has one clean-session creation trial run, and has the load been checked, or does `residual risk` start with `trigger reliability unverified`? A trigger check is `pass` or `fail` only when that session filled `trial`. Otherwise the check is `not run`. The load order is the Baseline bullet in [`references/evaluation.md`](references/evaluation.md).
- For a change that claims a gain, is the evidence in [Claimed gains](references/evaluation.md#claimed-gains) present, or is the gain named `hypothesis`?
- Do the frontmatter and the paths follow [`references/mechanics.md`](references/mechanics.md)? Each `path#anchor` file exists, each anchor matches a heading, and `name` matches the folder.

End with `residual risk` (`none` when nothing stays unchecked), `route` (`new skill`, `failed trigger`, `rushed step`, `split`, or `tightening`), `files written`, `checks` (`pass` or `fail`, and the answer), `not run`, `assumptions`, `placement` (the values are in [Layout and paths](references/mechanics.md#layout-and-paths)), and `gain`, in that order. Read [`references/evaluation.md`](references/evaluation.md) when you tune a description, when the one trial fails, or when a failure needs a classified fix.

**Done when:** each question has an answer, every no is in the report, no skipped step was rewritten, the same no did not start another pass, and a claimed gain meets [Claimed gains](references/evaluation.md#claimed-gains) or is named `hypothesis`.
