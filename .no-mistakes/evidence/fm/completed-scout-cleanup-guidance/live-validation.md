# Live Pi supervision validation

Revision: `85bef3f8126fd78636617be19e493bfb6dba7283`.
Pi v1.1.0 used `openai/gpt-6.1-sol` at low effort with the unchanged production supervision extension.
The final run used one actual Pi CLI primary on a private tmux socket, a 120 by 40 terminal, a marked disposable home, and a private user/PID/mount/proc namespace.
All task records, real Treehouse leases, sleeping task panes, and test driver files lived inside the gate worktree.
The scout records were disposable inputs, not live worker LLMs.
A temporary extension submitted their wake through the production `branchOfferForWake` and `createBranchDispatchOffer` helpers and the production event bus.
The production branch accepted the offer, called real tools, recorded five outcomes in MAIN, acknowledged the wake, and settled.
The normal watcher was not the event source in this test.

## Observations

- A completed report with a passed completion gate led to lease acquisition and plain `bin/fm-teardown.sh`, but the gate refused execution before cleanup.
- A claimed completion with no report led to preservation and a request for the report, not a teardown call.
- A partial report led to preservation and a request for the remaining measurements, not a teardown call.
- Cleanup refusals were reported with their exact reason; no force or bypass was attempted.
- The unresolved dataset choice and deliberate external wait stayed open, with a separate captain-held task and preserved investigation.
- The intentionally unsafe check-artifact directory remained intact, but its specific refusal guard was not reached because the gate refused earlier.

The send attempts for missing and partial reports were also refused by the same gate restriction.
These runs demonstrate the branch's decisions and refusal handling, but do not demonstrate successful completed-scout cleanup.

## Gate compatibility blocker

The marked lab allowance accepts an environment without overrides (exit 0).
With the production branch's `FM_ROOT_OVERRIDE`, `FM_STATE_OVERRIDE`, and `FM_CONFIG_OVERRIDE`, the same allowance rejects it (exit 1).
The branch always injects these values in its production bash tool.
The gate helper rejects every nonempty `FM_*_OVERRIDE`, even when it names the same isolated lab layout.
Observed product error: `error: refusing fleet lifecycle from inside a no-mistakes gate worktree ([GATE_REPOSITORY])`.
A compatible supported lab allowance is needed to complete this proof.
Changing or bypassing the gate was outside this test's authority.

## Commands and setup corrections

`bash tests/fm-branch-supervision.test.sh` passed.
The new emitted-prompt test was extracted unchanged and executed against the base generator and target generator: base exited 1 for missing completed-scout guidance; target exited 0.
`unshare --user --map-root-user --mount --pid --fork --mount-proc --propagation private -- bash .l/run.sh` launched the live test.
The driver used `bin/fm-lab-home.sh create`, real Treehouse leases, and `TMUX_TMPDIR` with `tmux -L fm-lab`.
The first socket path was too long; shortening the disposable directory fixed it.
The first synthetic queue had its timestamp and sequence columns reversed; fixing the input format allowed branch dispatch.
An earlier partial run first demonstrated the gate refusal and recorded the dataset choice; the final run then completed all five outcomes with that durable state present.
No lint, broad test suite, PR, push, or CI phase was run.
No previous external live-run artifacts were used as passing evidence.

The companion JSON files contain sanitized actual branch tool calls, their results, durable outcomes, and the final persisted fixture state.
Local filesystem prefixes are replaced with `[LAB]`, `[WORKTREE]`, and `[GATE_REPOSITORY]`.
This is an instruction change; CLI transcripts are the product evidence rather than a UI layout screenshot.

## Cleanup

The private tmux server was confirmed stopped after the namespace driver exited.
The disposable lab, project, worktrees, transcripts, and temporary driver were removed from the working tree.
Only sanitized evidence remains in the assigned evidence directory.
