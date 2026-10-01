---
name: pr-remediate
description: "Repair explicitly selected categories of the current user's open GitHub pull requests, such as conflicts, CI failures, or requested changes. Starts from fresh triage and never merges, deletes branches, or force-pushes without explicit authorization."
---

# PR Remediate

Repair only the pull requests and blocker categories the user explicitly selects. Start with fresh `pr-triage` data so remediation is based on current GitHub state.

## Scope

The request must identify PRs, repositories, or triage categories. Before modifying anything, state the selected PRs, the active blockers to address, and any requested exclusions.

Work on one PR at a time in a dedicated checkout or Git worktree. Preserve the user's existing worktrees and unrelated changes.

## Route each blocker

### Conflicts

Use `resolving-merge-conflicts` only after a merge or rebase conflict is in progress. Resolve the conflict from the relevant commits, preserve both compatible intents, and run the repository's checks.

Default to a normal push after a merge-based resolution. Begin a rebase only when the user explicitly authorizes it; force-push after a rebase only with separate explicit authorization.

### CI failures

Read the failed check logs first. For a clear, narrow failure, make the smallest repair and run the relevant local check. For an unclear, flaky, or substantive failure, use `diagnosing-bugs` to establish a tight feedback loop before changing behavior.

Use `tdd` for behavior changes only after agreeing the test seam. Do not add tests for mechanical formatting, configuration, or merge-only repairs unless they protect a real behavior.

### Requested changes

Read the review feedback and implement only clear requests. Surface ambiguous, contradictory, or product-direction feedback for the user rather than guessing. Use the same CI-failure routing when a requested change is substantive.

## Verify and publish

Run the relevant local checks after each repair. For a meaningful behavioral change, use `code-review` against the pre-remediation commit when its required spec and repository configuration are available; otherwise state that review was not run.

Commit only the repair for that PR and push it. A normal push is allowed by a request to repair a selected PR; force-push requires the explicit authorization stated above.

Re-run `pr-triage` after the selected repairs and report changed blockers, checks still pending or failing, and items needing human direction.

## Completion boundary

Finish after every selected PR is either repaired and rechecked, or clearly reported as requiring user direction. Merging, closing PRs, deleting branches, changing reviewers, posting comments, rerunning remote checks, and acting on drafts require separate explicit requests.
