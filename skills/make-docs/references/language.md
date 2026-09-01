# Language lock

One human language per suite. Load this file in confirm, generate, and verify.

## Who decides

1. The user named a language in this conversation: that lock wins.
2. Else the voice hunter's `language_candidate` when `mix_detected: no` and sources exist.
3. Else ask. A mix or a missing majority is a confirm unknown. Do not average languages.

## What stays in source form

- Identifiers, file paths, commands, flags
- BCP 14 keywords (next section)
- Code fences and Mermaid node IDs that match symbols in the tree

Headings, text, table cell text, and scenario text use the locked language.

## BCP 14 keywords

Requirement keywords follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html) as updated by [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174.html). They stay English. They carry requirement force only in ALL CAPS. The same words in lowercase are ordinary text in the locked language.

Tokens: MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, NOT RECOMMENDED, MAY, OPTIONAL.

Each spec file includes the incorporation sentence from `./references/template-spec.md` near the top.

## Inheritance

- **explore:** lock from voice sources, or the user's named language.
- **update** and **refresh:** inherit the language already used in `docs/`. The chat language does not override unless the user asks to switch.
- **adr:** same lock as the suite.

## Completion (for the phase that loaded this file)

Exactly one language tag is recorded. Text in files written this run matches that tag. Source-form tokens above are unchanged.
