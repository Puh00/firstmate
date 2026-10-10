# Completed-scout live validation

Tested revision: `6be22f9d92bf5c8949f61119224854d522ed6d69`.
The tracked source was unchanged throughout this test phase.

The two targeted regression scripts passed: `bash tests/fm-gate-refuse.test.sh` and `bash tests/fm-branch-supervision.test.sh`.
Direct calls to the real `bin/fm-send.sh` refused escaped state paths, alternate roots, unsupported overrides, noncanonical paths, symlink homes and stock directories, and missing, invalid, or symlinked lab identities.
These calls returned exit 3 before steering.

## Live execution

One real Pi primary per attempt used `openai/gpt-6.1-sol`, low effort, and the unchanged production supervision extension.
A fixture tool delivered five synthetic wakes through the production dispatch interface.
The normal watcher was not the event source.
The final attempt ran in private user, PID, mount, and proc namespaces, with private temporary storage and worktree-backed Pi and Herdr overlays.
The named non-default Herdr session was provisioned and torn down through the repository helper.
Its combined cleanup trap exited 0, including the default-session tripwire check.
The incoming pipeline marker remained present, no guard bypass was used, and Git source provenance remained a managed gate worktree.

Independent state assertions and real endpoint queries confirmed:

- Completed scout metadata and endpoint were removed, with the endpoint returning `pane_not_found`; its report and three-entry finding remained.
- Missing report stayed missing; task metadata and endpoint remained.
- Partial report stayed partial; task metadata and endpoint remained.
- Unsafe check-artifact symlink caused `REFUSED: unsafe task PR-check artifact; preserving task state.`; the symlink, protected target, report, metadata and endpoint remained.
- Unanswered dataset choice remained open through the real hold interface; the deliberate external wait, input status, report, metadata and endpoint remained.

## Reporting failure

The completed-scout outcome incorrectly states: "The report was retained and teardown reported success, although endpoint lifecycle control emitted a lab-home refusal."
The actual tool output instead says `fm-gate-refuse: gate agent lifecycle permitted only against lab home [LAB]` followed by successful teardown.
There was no completed-scout gate refusal in that output, and independent endpoint queries confirmed removal.
The real unsafe-artifact refusal belonged to a different task and was correctly reported separately.

The unsupported refusal claim appeared in all three attempts.
The first two attempts had historical fixture-log exposure, which initially suggested contamination.
The final attempt removed historical fixtures and used private temporary storage, but reproduced the claim.
The reporting cause is not established; contamination alone does not explain it.
The final primary also received the incorrect branch outcome.
This reporting scenario fails despite the successful cleanup and preservation state assertions.

## Limits

Scout records and real Herdr shell endpoints were disposable fixtures, without scout worker LLMs.
No allocated pool slot was exercised, so pool-slot return is unproven.
The manual-backlog fixture does not prove automatic backend closure.
These observations do not prove universal model adherence.
This is a CLI and agent-output change; transcripts and persisted state are the evidence, with no rendered UI requiring screenshots.
No lint, formatter, static analysis, full suite, pipeline control, publication, or CI phase was run.
