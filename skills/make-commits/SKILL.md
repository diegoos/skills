---
name: make-commits
description: >-
  Draft a message, create a commit, or amend HEAD. Use when the user asks for a commit message, asks to commit, or asks to amend.
metadata:
  version: 0.3.0
  author: "Diego Oliveira"
  tags:
    - git
    - conventional commits
---

# Make commits

One **concern** per commit. Name the branch at the start: **draft** (the message only), **commit**, or **amend**.

**Invariants.** Leave git config untouched. A missing `user.name` or `user.email` stops the run before any commit. Hooks run. `--no-verify` only when the user asks for it. End at the local commit. NEVER run `git push`, including `--force`, even when the request also asks to push. A pull request or a reset needs its own request.

## Survey

Run in parallel:

```bash
git status --porcelain
git diff --staged
git diff
git log -5 --no-merges --format=%B
git rev-parse --abbrev-ref HEAD
```

The path set is the staged paths when the user says staged, the named paths when the user names them, otherwise every path in status. Read each untracked text file. Note a binary path.

**Done when:** the diff or the file contents of every path in the set have been read, the branch name is known, and Voice has the log's language, a `type:` prefix or none, and the verb shape — or the log is empty.

## Partition

A **concern** is one reason the change exists. One group per concern. A rename stays one path, in the group that owns the new path.

Apply in order:

1. **Out.** A private key, a credential, or an env file that holds a secret stays out. A path the user excluded stays out.
2. **Single.** The user asked for one commit → one group of every path still in. Skip Together and Apart.
3. **Together.** A path with no meaning without another joins it: the test for this fix, the type this call needs, the changelog line for this change, the lockfile for this dependency, or the doc that only describes this change. A behavior-preserving refactor is its own concern.
4. **Apart.** Each remaining set a reviewer could merge on its own is a group. A file whose hunks belong to two groups joins the larger hunk. A group that another group needs comes first.

A path that still fits two groups after Together and Apart → ask once which group, then wait. Use the harness question tool, or chat when that tool is missing. That turn stops before any commit.

**Done when:** every path in the set is in exactly one group, or listed with the reason it stayed out. No path remains → Reply.

## Message

The message describes that group's diff. **Voice** picks the language and the shape. First match wins.

**Concise.** The subject is one clause of at most 72 characters. The body adds only the why that clause cannot hold.

1. **Ask.** Wording, language, or subject shape the user named. A part left open follows Log, then Default.
2. **Log.** A shared set is at least three of the last five non-merge subjects, or every subject when fewer than three exist, with one language and one `type:` prefix choice (present or absent). The latest subject in that set sets verb shape, case, emoji, scope, trailers, and a trailing period. Keep a `type:` prefix, in that language and verb shape (`chore: updating docs`, `feat: improve performance on home page`). The type is one that set already uses; a concern with none there uses Types. No shared set → Default.
3. **Default.** [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). Lowercase imperative, a `type:` prefix, no emoji, no trailing period. Scope only when two groups would share a subject without it.

A `type:` subject uses the block below. No `type:` in the log → that log's subject shape.

```text
<type>[optional scope][optional !]: <description>

- [optional body]

[optional footer]
```

**Type** is the group's concern. A supporting path takes that concern's type. A test-only change is `test`. A docs-only change is `docs`. A format-only change is `style`.

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.

**Body.** The why, when the subject does not carry it. Required for a breaking change, a security fix, a data migration, or a revert. A revert names the reverted subject or sha. A second concern, or a smaller hunk in the same file, is named in the body. Wrap at 72 characters. Sentences. A `-` list when the caller has steps.

**Breaking.** On a `type:` subject, `type(scope)!:` plus a `BREAKING CHANGE:` footer. The body says what the caller must do.

**Footer.** `Closes #n` or `Refs #n` uses a number the request or the branch name already states. Any other trailer matches the log.

Default:

```text
fix: validate the session before refresh

- A refresh on an expired session minted a token for a signed-out user.
```

## Branch draft

One message per group, from Message. Unstage a staged path that Out drops (`git restore --staged -- path…`). Leave every other path as it was at survey.

**Done when:** each group has a message, and `git status --porcelain` matches the survey except for a path Out unstaged.

## Branch commit

Commit the groups in Partition order. For each group, the index holds only that group's paths: unstage any other staged path (`git restore --staged -- path…`), then stage the group (`git add -- path…`). Replace `type: subject` with that group's message. A body follows a blank line when Body requires one.

```bash
git commit -m "$(cat <<'EOF'
type: subject
EOF
)"
```

Record the short hash (`git rev-parse --short HEAD`).

A hook that exits non-zero: stage this group's paths again and create a new commit. The same group failing twice stops the run. Report the hook output.

A hook that exits zero and leaves edits on files from the commit just created: those files go through Branch amend once. A stop in Branch amend stops this run.

**Done when:** each group has a commit, and `git status --porcelain` lists only paths that stayed out.

## Branch amend

Amend when both are true: this conversation created HEAD, and HEAD is unpushed (`git status -sb` has no upstream, or the branch shows `ahead`). Otherwise stop and report which check failed.

Stage paths the user named, or edits a hook left on files in HEAD (`git add -- path…`). A path that Out drops stays unstaged. Any other dirty path stays unstaged.

The user asked for a new message → write it from Message and replace `type: subject`:

```bash
git commit --amend -m "$(cat <<'EOF'
type: subject
EOF
)"
```

Otherwise `git commit --amend --no-edit`.

A non-zero hook stops the run. Report the hook output.

**Done when:** HEAD's subject is the new message, or the previous subject when the message was kept, and `git status --porcelain` lists only paths that stayed out.

## Reply

Each group, in commit order. **Draft:** the full message. **Commit:** the recorded short hash and the subject. **Amend:** `git rev-parse --short HEAD` and the subject. Then each path that stayed out, and why.

No path remains → there is nothing to commit. Still name each path that stayed out, and why.

**Done when:** every group and every path that stayed out appears in that form.
