# PR Remediate Codex Skill

`pr-remediate` repairs explicitly selected blockers on the authenticated GitHub user's open pull requests, including conflicts, CI failures, and requested changes.

## Install

In Codex, install this skill from this repository, then invoke it with `$pr-remediate` and identify the pull requests or blocker categories to repair.

## Safety

The skill begins with fresh triage and only addresses selected pull requests. It never merges, deletes branches, or force-pushes without explicit authorization.

See [SKILL.md](SKILL.md) for the complete workflow and safety boundary.
