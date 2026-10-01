# PR Remediate Codex Skill

`pr-remediate` repairs explicitly selected blockers on the authenticated GitHub user's open pull requests, including conflicts, CI failures, and requested changes.

## Install

In a Codex chat, ask the built-in installer:

> `$skill-installer install the skill from https://github.com/cdracars/pr-remediate/tree/main/skills/pr-remediate`

The skill will be available in your next turn. Invoke it with `$pr-remediate` and identify the pull requests or blocker categories to repair.

For a manual installation, copy `skills/pr-remediate/` into `~/.codex/skills/pr-remediate/`.

## Dependencies

`pr-remediate` relies on the following companion skills when the selected blocker calls for their remediation route. Install them to use every route:

- `resolving-merge-conflicts` for an in-progress merge or rebase conflict
- `diagnosing-bugs` for unclear, flaky, or substantive CI failures
- `tdd` for behavioral repairs after the test seam is agreed
- `code-review` for meaningful behavioral changes after remediation

These dependencies are available from [Matt Pocock's skills collection](https://github.com/mattpocock/skills). The PR triage and straightforward remediation paths do not invoke them.

## Safety

The skill begins with fresh triage and only addresses selected pull requests. It never merges, deletes branches, or force-pushes without explicit authorization.

See [the skill instructions](skills/pr-remediate/SKILL.md) for the complete workflow and safety boundary.

## License

This project is licensed under the [MIT License](LICENSE).
