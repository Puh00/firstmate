# Cleanup reporting validation

The supervisor previously reported a lab-home refusal although cleanup succeeded.
The saved failing transcript shows multiple tasks handled in one shell call, with an allowance diagnostic and another task's actual refusal in the same output.
A fresh unchanged live run passed, so the reporting defect is intermittent and batching alone does not establish its cause.
The narrow correction requires separate cleanup calls and task-specific exit/output attribution, distinguishing permission diagnostics from refusals.
No guard, cleanup implementation, production integration, or external infrastructure was changed.

## Verification

- `bash tests/fm-branch-supervision.test.sh`: new generated-interface assertion failed before the prompt correction; the focused script passed afterward with exit 0.
- `LIVE_CASE=before unshare --user --map-root-user --mount --pid --fork --mount-proc --propagation private -- bash .test-evidence/driver.sh`: passed with unchanged source; this attempt did not reproduce the intermittent reporting failure.
- The same command with `LIVE_CASE=after`: passed with the correction, using the real Pi primary, unchanged production supervision extension, GPT-6.1 Sol, real named Herdr lab endpoints, and the marked disposable-home allowance.
- The incoming gate marker remained present, bypass remained inactive, and managed Git provenance was confirmed.
- Real tool calls were separate: `bin/fm-teardown.sh complete` succeeded and `bin/fm-teardown.sh refusal` returned the specific unsafe task PR-check artifact refusal.
- Independent endpoint queries confirmed the completed endpoint was absent and the other four remained present.
- The completed report and finding remained; missing and partial reports, the unanswered dataset choice, deliberate external wait, unsafe artifact link and protected file remained intact.
- The completed outcome stated that cleanup succeeded without inventing a refusal; the refused task reported its actual reason.
- Both combined cleanup traps completed with exit 0, including the helper's default-session tripwire check.

## Tested source

HEAD: `6be22f9d92bf5c8949f61119224854d522ed6d69`.
Applied patch SHA-256: `e8ac2682d38f80f12319af77329348730ff1ead8965f2874b38d4b94302689db`.
The outer executor owns committing these changes; `cleanup-report-tested-source.json` records exact tested file hashes.
The `cleanup-report-after-*` records retain sanitized actual branch and primary transcripts, outcomes, endpoint queries, state, driver, guard output and cleanup evidence.
The `cleanup-report-before-*` records retain the fresh pre-fix observation, not a claimed failure.

## Limits

This prompt correction is supported by one passing post-fix live evaluation, not proof of universal model adherence or deterministic elimination of the intermittent failure.
No allocated pool-slot return was tested.
Incomplete task fixtures had exited agents and unavailable recorded working copies, so steering was durably saved but delivery/recovery was refused; preservation, not successful resumption, was the expected scenario.
The shared prompt serves Pi and the supervision host, but this live evaluation used Pi only.
No lint, formatter, static analysis, complete repository suite, publication, PR update, CI action or other pipeline phase was run.
The outer executor must retain these limits when updating the PR testing narrative and run its remaining required phases.
