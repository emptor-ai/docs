# Self review

Every PR must complete **Self review** before it is handed to a teammate. This
applies to all changes, including documentation and follow-up commits.

## Before PR handoff

1. **Review the complete change.** Confirm the PR's actual target branch and fetch
   its current state. Review the full diff from its merge base to the proposed
   head, including committed changes, staged and unstaged edits, and new files
   intended for the PR. Do not rely on a plain `git diff` or assume the target is
   `main` or `master`. Read surrounding code and relevant callers as needed.
2. **Run the Ponytail complexity pass.** Use the `ponytail-review` skill if
   available, explicitly giving it the full PR scope. Otherwise read and apply
   the pinned Ponytail rubric below directly, and describe it as an
   instruction-based Ponytail review. Never claim a plugin or command ran if it
   did not. Record concrete findings with file locations, or state that no
   unnecessary complexity was found.
3. **Check correctness separately.** Review behavior, regressions, error handling,
   security, performance, and accessibility where relevant. Ponytail's complexity
   verdict is not evidence that these checks passed. Preserve necessary
   validation, authorization, error handling, and tests when simplifying code.
4. **Resolve findings and verify.** Make clear, in-scope fixes and run the checks
   appropriate to the final change, following the repository's existing test
   requirements. Documentation-only changes need a content/link/diff check, not
   invented application tests. Explain any finding intentionally retained or
   deferred and its risk; use existing ticket/decision rules. If a material
   finding or required check remains unresolved, report it and keep the PR draft.
5. **Review the final version.** Recheck after fixes. Record the reviewed head
   commit and target branch commit once the intended changes are committed.
   Any subsequent commit, included working-tree edit, or target-branch change
   makes the record stale: inspect the updated full PR diff, repeat the relevant
   review and checks, and refresh the record before another handoff.
6. **Record and hand off.** Include a short `Self review` section in the PR
   description (or the prepared description if publishing is not authorized).
   State the reviewed head/base commits, Ponytail outcome, correctness outcome,
   checks actually run and their results, and any retained findings with reasons.
   Do not expose secrets or sensitive test data in the record.

Complete this sequence before creating a ready-for-review PR, marking a draft
ready, requesting or re-requesting a teammate's review, or reporting a PR ready
for human review. If changes must be pushed earlier for backup or CI, keep the PR
draft and do not request reviewers. Completion does not itself authorize a push,
review request, merge, or message; follow the user's existing authorization.

This is an agent workflow requirement. It does not install GitHub checks or
change branch protection, and it does not replace human review.

## Ponytail complexity rubric

Adapted from [Ponytail's review instructions](https://github.com/DietrichGebert/ponytail/blob/356918eba965ee1eac64bd3a7f0dd02108350de5/skills/ponytail-review/SKILL.md),
pinned to commit `356918eba965ee1eac64bd3a7f0dd02108350de5`.

Look for unnecessary complexity in the full PR diff:

- `delete`: dead code, unused flexibility, or speculative features.
- `stdlib`: custom code duplicating a standard-library facility.
- `native`: custom code or a dependency duplicating a native platform feature.
- `yagni`: speculative abstractions, unused configuration, or unnecessary layers.
- `shrink`: a smaller, equally correct and readable implementation.

For each finding, give its file and line, category, what could be removed, and
what would replace it. Read the context before recommending a deletion. A
single smoke test is useful verification, not bloat. Do not remove necessary
behavior merely to reduce line count. Report estimated removable lines only
when supported by the findings; if nothing should change, say so.

Ponytail identifies complexity and suggests changes. Apply and validate accepted
fixes in the subsequent step. Keep correctness, security, and performance findings
in the separate correctness pass.

## Ponytail license

MIT License

Copyright (c) 2026 DietrichGebert

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
