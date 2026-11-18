# Release Field Skills

Three agent skills for the gap between “the tests passed” and “this works for someone who already uses the software.”

| When you need to know… | Use |
|---|---|
| Can a user install this build or update to it? | [Verify the shipped artifact](skills/verify-shipped-artifact/SKILL.md) |
| Does the published number describe the program we ship? | [Reproduce a benchmark claim](skills/reproduce-benchmark-claim/SKILL.md) |
| Will an older client or an existing file still work? | [Check the upgrade contract](skills/check-upgrade-contract/SKILL.md) |

## Try one

Copy the skill directory you need into your project's `.claude/skills/` directory. In Claude Code, ask:

> /check-upgrade-contract The new reader opens files written by the new writer. Check whether it also reads a file written by the last release.

The skills use the [Agent Skills format](https://agentskills.io/specification). Each is a standalone Markdown file. They don't install hooks, upload logs, or deploy anything. You can also read one as a checklist without an agent.

[MIT license](LICENSE)
