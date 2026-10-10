# Test phase recheck

The current revision is `85bef3f8126fd78636617be19e493bfb6dba7283`.
No source files were changed and no live primary was launched in this recheck.

The existing `test_branch_prompt_routes_completed_scouts_through_guarded_cleanup` function was executed in Bash with its assertion helpers against the real `bin/fm-branch-prompt.sh` generator.
It passed.
This verifies the emitted instruction contract only, not model adherence or successful cleanup.

The existing guard-context comparison and live-validation evidence were read.
Current production `scriptEnv` still unconditionally supplies `FM_ROOT_OVERRIDE`, `FM_STATE_OVERRIDE`, and `FM_CONFIG_OVERRIDE`.
The marked-home allowance still rejects every nonempty `FM_*_OVERRIDE`.
Neither implementation is changed by the target commit.
The recorded prior guard probe permitted the stock marked home and refused the production branch environment with exit 3.
The supplied decision explicitly forbids repeating blind attempts or changing this guard contract in this phase.
Consequently the known blocked primary launch was not repeated.

The earlier successful run used a different source location and cleared the gate marker.
Its historical incoming gate-marker state and git-common-directory provenance were not recorded in the comparison evidence, so its preservation of every applicable guard cannot be certified.
The earlier results are not counted as live passes in this recheck.

A separately authorized compatibility change between the production branch environment and marked-lab allowance is required before rerunning successful cleanup and the unsafe-artifact-specific refusal under this gate.
That change must retain refusal of paths outside the disposable lab.
Incomplete-report and unanswered-choice observations remain historical evidence, not fresh executions.
No lint, broad suite, pipeline control, external publication, or shared-fleet operation was performed.
No transient worktree files were created.
