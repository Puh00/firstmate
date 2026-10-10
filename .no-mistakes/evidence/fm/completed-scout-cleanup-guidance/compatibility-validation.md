# Supervision lab compatibility validation

The focused regression and all five live scout scenarios passed on 2026-10-10.
The production Pi supervision integration was unchanged.

## Tested source

The run used managed gate HEAD `85bef3f8126fd78636617be19e493bfb6dba7283` plus the compatibility patch with SHA-256 `b388bfc867f0f0b939e9c73e84829e830e5ad57a19850a602b20d705b910ba76`.
`compatibility-tested-source.json` records each changed file hash.
The outer executor owns committing this patch and binding the resulting commit to this evidence; no new commit SHA existed during the test.
Subsequent source changes require the relevant verification to be refreshed.

## Reproduction and correction

The actual guard exited 3 with a freshly marked lab and the production branch's root, state, and config overrides.
The executable regression failed before the fix with `expected exit 0, got 3`, then passed afterward.
It invokes the real guard under `set -eu` and verifies stock paths plus refusal of unmarked homes, invalid or symlinked markers, symlinked stock directories, noncanonical homes, redirected paths, and unsupported overrides.
The correction accepts only redundant production root/state/config overrides after canonical path checks; every other nonempty override still refuses.
The code root is derived from the loaded tracked library independently of the override.
The existing regression helper removes its test-harness bypass before invoking the guard.
No gate marker was stripped, no bypass was used for live execution, and source was not relocated.

## Actual live observations

One real Pi CLI primary, Pi 1.1.0 with `openai/gpt-6.1-sol` at low effort, handled the final run.
An injected test tool offered synthetic wakes through production `branchOfferForWake`, `createBranchDispatchOffer`, and the event bus.
The production branch accepted them, acquired leases, called ordinary tools, recorded five durable outcomes, and delivered them to MAIN.
MAIN acknowledged them through production `fm_branch_processed`.
The normal watcher was not the event source.

- Completed scout: ordinary teardown succeeded; endpoint and metadata were absent afterward, and its report and finding remained.
- Missing report: no report was fabricated; metadata and endpoint remained, and a report request was recorded.
- Partial report: report, metadata, and endpoint remained, with a request to finish the observations.
- Unsafe artifact: teardown returned `REFUSED: unsafe task PR-check artifact; preserving task state.`; the symlink, protected content, metadata, and endpoint remained.
- Unanswered choice and deliberate wait: report, input status, metadata, and endpoint remained; the production hold interface confirmed the dataset decision still open.

The entire primary, branch, task, and named non-default Herdr lab process tree ran in private user/PID/mount/proc namespaces.
Private mount overlays redirected Herdr and Pi writes into worktree-backed directories while keeping the real default-session tripwire readable.
The incoming gate marker remained present and the source remained a managed gate worktree.
The production guard explicitly accepted the confined branch paths.
Independent state assertions passed, and the combined EXIT trap completed guarded lab teardown and its default-session tripwire check.
A subsequent external read-only inventory showed only the unchanged running default session.

## Limits

Scout records and real Herdr shell endpoints were disposable fixtures, without scout worker LLMs.
No allocated pool slot was used; pool-slot return is unproven.
This is one empirical model run, not universal model-adherence proof.
The manual-backlog fixture did not test automatic task-backend closure.
Earlier fixture iterations exposed a missing initial workspace and incomplete endpoint metadata; those runs were not counted as passes and their cleanup traps ran.
Historical outside-pipeline observations were not substituted for this run.
No lint, formatter, static analysis, broad suite, pipeline control, publication, CI, or merge was performed.
Temporary fixtures and copied runtime state are removed after evidence export.

## Evidence

The `compatibility-regression-before.log` and `compatibility-regression-after.log` files retain the focused regression result.
The `compatibility-branch-transcript.json`, `compatibility-primary-transcript.json`, and `compatibility-branch-outcomes.jsonl` files retain sanitized actual calls, results, and outcomes.
Large discovery output and model thinking blocks are omitted; lifecycle calls and results remain.
The `compatibility-state.json`, `compatibility-assertions.json`, `compatibility-guard.log`, and `compatibility-cleanup.log` files retain state and cleanup evidence.
