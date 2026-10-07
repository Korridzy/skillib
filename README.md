# skillib

Portable skills for coding agents, starting with a project-aware `/issue` workflow.

## Issue drafting

The [`issue` skill](skills/issue/SKILL.md) drafts one implementation-ready GitHub
issue title and body. It reads the project where you invoke it: applicable agent
instructions, contribution guidelines, issue templates, relevant code, and tests.
The draft includes concrete acceptance criteria and a focused validation plan.

It only drafts. It does not implement the task, edit files, or post anything to
GitHub. No GitHub account, CLI, or MCP server is needed for drafting.

| Skill | Purpose |
| --- | --- |
| [`issue`](skills/issue/) | The read-only `/issue` drafting workflow, with its own bundled templates |
| [`github-issues`](skills/github-issues/) | The corresponding issue-management skill and all ten reference files |

Install `issue` for drafting. The separate `github-issues` skill also describes
remote writes; use it when you explicitly want to manage issues. Its operations
need an authenticated GitHub CLI or the relevant GitHub MCP tools. MCP tool names
vary by agent; discover the equivalent tools or use the documented CLI/API path.

## Install

Both skills follow the [Agent Skills specification](https://agentskills.io/specification).
The [skills CLI](https://github.com/vercel-labs/skills) installs them into supported
agents' discovery directories.

Install the drafting skill globally and choose your agents:

```sh
npx skills add Korridzy/skillib --skill issue --global
```

Or install globally for these common agents without prompts:

```sh
npx skills add Korridzy/skillib --skill issue --global --agent claude-code codex opencode cursor gemini-cli --yes
```

To install only for the current project, omit `--global`. Target every configured
agent integration in the current project:

```sh
npx skills add Korridzy/skillib --skill issue --agent '*' --yes
```

The installer can skip agent-specific project directories that do not exist.
Create the agent's project configuration directory and rerun, or use the manual
installation below. Eve and PromptScript support project installation only;
including them in a global `--agent '*'` installation reports those two failures.

List the available skills, or install the corresponding management skill:

```sh
npx skills add Korridzy/skillib --list
npx skills add Korridzy/skillib --skill github-issues --global
```

Installing a skill does not give every agent the same slash-command interface.
Use the invocation supported by your agent, or the standalone prompt below.

## Use

Start the agent in the project the proposed issue concerns. For Claude Code:

```text
/issue Add CSV export to the reports page
```

For Codex:

```text
$issue Add CSV export to the reports page
```

For other agents, select the installed `issue` skill or ask:

```text
Use the issue skill to draft an issue for adding CSV export to the reports page.
```

With no task description, the workflow asks what you want to describe rather than
guessing from earlier conversation.

### Keep the literal /issue command

[`commands/issue.md`](commands/issue.md) is a self-contained Markdown command
using `$ARGUMENTS`. [`commands/issue.toml`](commands/issue.toml) contains the same
prompt with Gemini CLI's `{{args}}` substitution.

Copy the appropriate file to your agent's command directory:

| Agent | Global destination | Project destination |
| --- | --- | --- |
| Claude Code | `~/.claude/commands/issue.md` | `.claude/commands/issue.md` |
| OpenCode | `~/.config/opencode/commands/issue.md` | `.opencode/commands/issue.md` |
| Gemini CLI | `~/.gemini/commands/issue.toml` | `.gemini/commands/issue.toml` |
| OmO/Senpi | `~/.omo/agent/prompts/issue.md` | Use the global prompt or the agent's configured prompt directory |

Claude Code already exposes `/issue` when the `issue` skill is installed; choose
the skill or the command file, rather than installing both under the same name.
Restart or reload the agent if newly installed commands do not appear.

Command formats: [Claude Code](https://code.claude.com/docs/en/skills),
[OpenCode](https://opencode.ai/docs/commands/),
[Gemini CLI](https://geminicli.com/docs/cli/custom-commands/).
Codex uses [skill mentions](https://developers.openai.com/codex/skills/) instead.

## Any other coding agent

No proprietary tool names or runtime are required by the drafting skill. If your
agent supports Agent Skills but is not listed by the installer, copy the entire
`skills/issue/` directory into its documented skill directory, including the
templates and license.

If your agent has no native skill or custom-command support, open
[`commands/issue.md`](commands/issue.md), replace `$ARGUMENTS` with your task, and
paste the Markdown body after the frontmatter into the agent's chat. Alternatively,
give it [`skills/issue/SKILL.md`](skills/issue/SKILL.md) and the task description.
The agent needs access to the target project's files, or you must supply that
context yourself. This makes the workflow usable as instructions even when native
skill discovery or `/issue` is unavailable.

## Source and license

The drafting workflow is adapted from Korridzy's global `/issue` prompt. Its
machine-specific skill path has been replaced with bundled templates in the
standard skill and an optional named skill in the standalone commands.

The `github-issues` skill and references were imported from the locally installed
skill originating in
[`github/awesome-copilot`](https://github.com/github/awesome-copilot/tree/main/skills/github-issues).
The drafting skill's fallback templates come from that skill.

MIT licensed. The repository [license](LICENSE) and licenses bundled with each
skill retain GitHub's copyright notice for the imported material.
