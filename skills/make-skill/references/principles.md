# Principles

This file is the authority for pointers, completion criteria, leading words, negation, pruning, and size. When [`SKILL.md`](../SKILL.md) and this file disagree on those topics, follow this file. Other sections are the test behind a decision [`SKILL.md`](../SKILL.md) states in one sentence. Read the section when you make that decision, or when a trial shows a rush, drift, or a missed trigger. Each section gives the force, the test, and what the test changes.

## Contents

- [What earns a skill](#what-earns-a-skill)
- [Two budgets](#two-budgets)
- [Pointers](#pointers)
- [Information hierarchy](#information-hierarchy)
- [Co-location and sprawl](#co-location-and-sprawl)
- [Size to the work](#size-to-the-work)
- [Completion criteria](#completion-criteria)
- [Splitting](#splitting)
- [Invocation and the human index](#invocation-and-the-human-index)
- [Leading words](#leading-words)
- [Negation](#negation)
- [Pruning](#pruning)

## What earns a skill

Depth for [Find the repeat](../SKILL.md#find-the-repeat). Read it when a request could be a prompt, always-on instructions, or a skill.

- **Repeat.** A skill pays for itself on the next run. A procedure that will not recur stays in the prompt, and the reply says so.
- **Evidence.** The test is whether a step names a decision this work gets wrong. Generic best practice fails the test.
- **Always-on.** The test is whether every run needs the fact, including runs that never fire the skill. Those facts belong in always-on instructions. A skill supplies a fact only on the runs that reach it.
- **Context names.** The test is whether the request named the repository, path, or file. Only then may the skill carry it, marked as that context's fact. A name the request did not give fails in the next context.
- **Missing source.** Write the steps the request covers, mark each step that depends on the missing source, and report the gap. Filling the source in teaches a false procedure.
- **One job.** The test is one sentence around one verb. Several jobs in one description give the agent more than one way to trigger, and it takes the wrong one. A split that makes two skills fight over the same job fails the test too.
- **Lifetime.** A rule that works around a current model limit is a capability. Review it when the model changes, because a limit the model no longer has is a no-op. A rule that records a process or domain knowledge is a preference, and it lasts until that process changes.

## Two budgets

**Context load** is the cost of what the agent holds on every turn, paid whether or not the skill fires. **Cognitive load** is the cost on the person, who must know that a skill exists and when to use it. Spend the person's attention where human judgment matters, and remove it where the agent can decide. Material with no pointer and no way to invoke it spends only cognitive load, so it stays unfound.

## Pointers

A context pointer names material outside the context and encodes the condition for reaching it. A skill's description is one. Its wording decides when the agent reaches the material, and how reliably. A pointer does two jobs: it states what the material is, and it lists the branches that should trigger reaching it. A branch is a distinct case the document handles, so different runs take different paths through it.

- Front-load the leading word. The pointer is where the word does its triggering work. In a description, that word is the verb that names the job.
- A branch is one path. Put every wording of that path in the same Use when clause. Keep a wording when cutting it would miss a real request, and cut a wording that only repeats one you kept.
- Cut identity that the body already states.
- A pointer that fails in some runs is a variance problem. Sharpen its wording first. Inline the material only if sharpening fails.

Each word of an always-loaded pointer costs context load on every turn, so prune it harder than the body.

## Information hierarchy

A skill has two content types. **Steps** are ordered actions. **Reference** is definitions, rules, and facts that the agent consults on demand. The two mix freely. Each piece sits on one rung, ranked by how soon the agent needs it:

1. An in-file step: the main tier, what the agent does in order.
2. An in-file reference: consulted on demand. A flat set of rules on one level is a legitimate arrangement, not a smell.
3. A disclosed reference: a separate file that a pointer reaches, loaded only when the pointer fires.

Push too little down, and the top bloats. Push too much down, and the agent misses what it needs. Disclosure protects the hierarchy; it is not mainly a token saving. The test is branching. Inline what every branch needs. Push behind a pointer what only some branches reach. Reference that sits between steps and buries them turns attention into chance, which is a variance problem as well as a readability problem.

## Co-location and sprawl

**Co-location** keeps a concept's definition, rules, and caveats under one heading, so that reading one part brings its neighbors with it. Scattering breaks a concept into fragments. Duplication repeats one meaning in two places. These are different faults. Co-location fixes scattering. Deleting one copy fixes duplication.

**Sprawl** is a document that is too long, even when every line is live and unique. Attention thins across the excess, and each extra line has to stay relevant. The cure is the hierarchy: disclose reference behind pointers, and split by branch or by sequence, so that each path carries only what it needs.

## Size to the work

Depth for [Structure the skill](../SKILL.md#structure-the-skill). Read it when you add or remove a file, or when a draft has an empty file.

An extra file keeps the quality floor.

An existing skill keeps the files the folder already has. The route applies the rules of each file that is present. Add a file when the user asked, or when the change does not fit the files the folder has. Remove a reference that never opens. When the user asked to simplify, remove the files the user named. A second pass of the gate keeps the files this run already chose.

Add `assets/` when a step needs a block the template leaves out.

- **`references/`.** Each file holds one concept, one folder below `SKILL.md`.

## Completion criteria

Every step ends on a completion criterion. Two properties decide whether it works.

- **Clarity.** Can the agent tell done from not done? A vague bound, such as "understanding reached", invites **premature completion**: the agent ends the step early. The visible steps still ahead pull its attention toward being done.
- **Demand.** How much work must the criterion force? Demand drives **legwork**, the search and checking the agent does inside the step. Legwork is latent in the wording. "Every modified model accounted for" calls for legwork. "Produce a change list" does not.

Demand also applies to reference-only sections. "Every applicable rule checked" sets the same bar for a body of flat rules that has no steps. The strongest criteria are both checkable and exhaustive.

## Splitting

Splitting spends one of two loads. A split adds files, which costs context load, or it asks someone to remember the split, which costs cognitive load. Split only when the cut earns that cost.

- **By sequence.** Split a run of steps when the later steps tempt the agent to rush the current one. Keeping them out of view drives legwork on the current step. The reverse holds too: merging sequences exposes each step to what follows, which invites premature completion.
- **By invocation.** Split off a model-invoked skill when a distinct trigger word should fire it on its own, or when another skill must reach it. Its description is always-loaded context, so the independent reach has to be worth the cost.

Hiding later steps needs a real context boundary, such as a handoff to a subagent. An inline call keeps the later steps in context, so it hides nothing.

## Invocation and the human index

A **model-invoked** skill keeps its description in context. The agent can choose it, another skill can invoke it, and the person can still type its name. The cost is context load on every turn. A **user-invoked** skill keeps a one-line `description` with no trigger list. The agent does not use that line to choose the skill, so the skill costs no context load, but the person is the only index that knows it exists, which is cognitive load.

Pick model invocation only when the agent, or another skill, must reach the skill. If the skill only fires by hand, make it user-invoked.

Two user-invoked skills cannot invoke each other. A **router** skill cures the cognitive load that piles up when many user-invoked skills exist. It is a user-invoked skill that names the others and says when to use each. It can hint, but it cannot fire them.

Shared reference between skills stays an open choice. A model-invoked skill that holds only reference can serve several skills the agent reaches. A plain file outside the skill system can serve skills that no skill system reaches. Pick the place that fits how the skills are invoked, and state the choice.

## Leading words

A **leading word** is a compact concept the model already holds from training, such as `tight`, `red`, or `tracer bullets`. Used as one token, it recalls a region of behavior in few tokens, because the model brings priors that a sentence would have to spell out.

- Prefer a word that already exists. An invented word brings no priors, so its definition costs tokens that a trained word gives free. Coin a word only when you define it clearly.
- A leading word anchors in two places. In the body, it sets the behavior the agent follows wherever the word appears. In a pointer, it links the agent's prompts, docs, and code, so the agent reaches the material more reliably.
- Look for restatements to collapse: a triad spelled out at several sites, or a pointer that spends a whole sentence on one idea. "Fast, deterministic, low-overhead" becomes `tight`.
- A word the model already obeys on its own changes nothing. Replace it with a stronger word, not with another technique.

## Negation

A prohibition steers by putting the forbidden behavior into context. The concept it names becomes more available. A negation is a weak modifier, so a strongly activated concept can overrun it. "Do not X" can then read as "do X".

State the target instead. "Write one-line comments" keeps the banned behavior unspoken. Keep a prohibition only as a hard guardrail that you cannot phrase positively, and pair it with the target, so attention lands on what to do.

## Pruning

- **Single source of truth.** Keep each meaning in one authoritative place, so a behavior change is a one-place edit. Duplicates cost upkeep and tokens, and they inflate a meaning past its real rank.
- **Environment and cache.** The environment is a source of truth too: package scripts, config files, the directory layout, `--help` output. A skill that restates it holds a cache. A cache earns its load only when the lookup is expensive. Keep what the agent cannot find by looking: the unwritten convention, the reason behind a choice, the gotcha that no config states. A correction the agent repeats is a gotcha.
- **Relevance.** A line loses relevance when it never bears on the task, or when the behavior it describes changes. A version, a date, or a price goes stale in the body. Shorter skills stay relevant more easily.
- **No-ops.** The test is whether the sentence changes behavior against the model's default, not whether the reader likes it. When two people disagree about a no-op, they disagree about the default, so settle it by running the skill. When a sentence fails, delete the whole sentence.
- **Sediment.** Prune on a schedule, and remove a rule that no longer changes a result. A layer that stays only because adding feels safe and removing feels risky is sediment.
