---
name: issue
description: Draft an implementation-ready GitHub issue title and body grounded in the current project's instructions, templates, code, and tests. Use for /issue, issue proposals, bug reports, feature requests, or task descriptions when the user wants a draft to review rather than an issue posted or work implemented.
license: MIT
---

# Issue

Draft one proposed GitHub issue for the task below, in the project where this
command was invoked. Produce a title and body for the user to review and copy.
This is a read-only drafting request: do not implement the task, modify files,
or create or update GitHub issues, comments, labels, or other remote resources.

## Task description

Use the task description explicitly provided with this skill invocation. If no
task description is provided, ask the user what task they want to describe and
stop. Do not infer a task from earlier conversation.

## Gather project context

1. Start from the invocation's current working directory, not the directory
   containing this command. Identify the repository root when available and the
   relevant package or subproject in a monorepo. Outside a Git repository, use
   the current project directory; GitHub access is not required to draft.
2. Read applicable project instructions and guidelines: `AGENTS.md` (including
   relevant nested instructions), `CLAUDE.md`, `.github/copilot-instructions.md`,
   applicable path-specific instructions, `README`, `CONTRIBUTING`, and relevant
   architecture or decision documents where present. Follow their scope and
   precedence; do not assume a missing file exists.
3. Inspect `.github/ISSUE_TEMPLATE/` and other documented issue templates or
   contribution conventions. Choose the template matching the task. For issue
   forms, carry the required fields into the Markdown body without inventing
   answers to satisfy them.
4. Inspect the relevant implementation, callers, tests, and configuration using
   the available code-navigation tools. Establish current behavior, existing
   patterns, likely affected components, constraints, and verification commands.
   Keep investigation proportional to the task; do not survey unrelated areas.
5. Read the bundled [issue templates](references/templates.md) when no project
   template fits. Use them as writing guidance, not as required headings or an
   instruction to create an issue. Project-specific templates and guidelines
   take precedence over generic examples.

## Define the proposed work

- Describe the actual problem or desired outcome, why it matters, and how the
  requested result differs from current behavior.
- Keep the scope limited to the user's task. State meaningful exclusions when
  they prevent ambiguity; do not add adjacent features or cleanup.
- Ground implementation guidance in observed project patterns, citing real
  repository-relative paths and symbols where useful. Distinguish confirmed
  facts from suggestions, assumptions, and unresolved decisions. Do not invent
  APIs, requirements, issue numbers, dependencies, or labels.
- Include concrete, observable acceptance criteria as unchecked checkboxes.
  Cover the primary behavior and relevant edge cases or compatibility needs;
  avoid vague criteria such as "works correctly."
- Specify a focused validation plan using the project's actual test, lint,
  build, or manual-check conventions. These are checks for the eventual
  implementation, not claims that you have run them while drafting.
- Mention dependencies, risks, rollout or migration needs only when supported
  by the task and project evidence.
- Resolve routine details from the project. If an unresolved decision
  materially changes the task, include a short, specific open question in the
  draft and clearly mark any affected assumption; do not silently decide it.

## Final deliverable

Return one proposed issue, not an implementation or a posted-issue confirmation:

**Title:** A specific, actionable title, preferably under 72 characters.
Follow the project's title conventions; do not add an issue-type prefix unless
the project requires one.

**Body:**
Use the selected project template's headings and required fields. Where no
template exists, use a concise structure covering:

- Summary and motivation
- Current behavior and relevant project context
- Proposed scope and implementation guidance
- Acceptance criteria
- Validation plan
- Dependencies or open questions, only when needed

Adapt the body to the task: include known reproduction steps and expected versus
actual behavior for bugs, or the desired user-visible outcome for features.
Place acceptance criteria and validation within the closest appropriate section
if a project template fixes the structure. Use the project's required language,
otherwise the user's language. Keep the body ready to paste into an issue, with
no empty boilerplate, fabricated evidence, or claims that an issue was created.
