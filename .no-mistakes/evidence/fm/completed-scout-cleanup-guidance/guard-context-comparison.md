# Live validation remains blocked

No source or guard changes were made.
Required successful cleanup and the unsafe-artifact-specific refusal were not driven again in this gate.
The selected finding remains unresolved; the previous live-test exception is not reinstated.

## Focused reproduction

The tested revision remains `85bef3f8126fd78636617be19e493bfb6dba7283`.
A fresh empty home was marked using the unchanged `bin/fm-lab-home.sh create` interface inside the gate worktree.
The unchanged `fm_refuse_if_gate_agent` function was then executed in subshells anchored to the current worktree, first with the marked stock home and then with the production branch environment.
No lifecycle action or server was started.
The existing gate marker was preserved and the bypass was unset throughout.

Observed output:

```text
NO_MISTAKES_GATE present: x
FM_GATE_REFUSE_BYPASS active: unset
gate context: env
stock marked-home guard exit: 0
production branch guard exit: 3
PASS: marked stock home permitted; production branch environment refused before lifecycle
```

The second case added `FM_ROOT_OVERRIDE` pointing to the current source and `FM_STATE_OVERRIDE` and `FM_CONFIG_OVERRIDE` pointing inside the same marked home.
The branch unconditionally adds these variables through its production `scriptEnv`.
The marked-home allowance rejects any nonempty `FM_*_OVERRIDE`, including these stock-layout values.
This is a validation setup incompatibility, not a reproduced failure of the changed cleanup instructions.
The temporary probe directory was removed through its EXIT trap.

## Prior versus current execution

The named authoritative prior run and this worktree record the same revision.
Its saved invocation loads the production supervision extension from a Treehouse checkout, with the primary working in a disposable home outside this gate worktree.
Its driver uses a private user/PID/mount/proc namespace, a named non-default Herdr lab and a combined cleanup trap.
Its initial process record contains only PID 1 bash and its ps child.
It launches one Pi CLI primary in JSON print mode and submits synthetic scout wakes through an injected extension and the production event bus.
The recorded model is `openai/gpt-6.1-sol`.
The earlier gate attempt instead used a private tmux primary and Treehouse leases within this gate worktree, preserving the gate restriction.
Transport differs, but the reproduction above shows the refusal depends on gate context and branch overrides before either backend can perform cleanup.

The original driver explicitly unsets `NO_MISTAKES_GATE` and `FM_GATE_REFUSE_BYPASS`, along with inherited task and path variables, before launching the primary.
Its native driver then sets `FM_ROOT_OVERRIDE` to the lab home and the production branch adds the state and config overrides.
The original source location differs from this gate checkout, whose gate classification has an independent git-location backstop.
The current process also has `NO_MISTAKES_GATE` set.
Clearing that marker or moving source to evade the backstop is prohibited and was not attempted.
The saved artifacts do not include the original incoming gate-marker presence or historical git-common-dir provenance.
Consequently, the earlier run cannot be certified as having preserved every guard applicable to its incoming environment.
An unset operation alone does not prove the variable was previously set, so it also does not prove an actual historical bypass.

## Saved evidence examined

The prior primary invocation, actual primary session, persisted branch session, deliveries, outcomes, state assertions, revision and cleanup log were inspected directly.
The branch transcript records ordinary completion-gate verification followed by `fm-teardown.sh synthetic-completed` and a successful teardown result.
It separately records ordinary teardown for the unsafe-artifact fixture returning `REFUSED: unsafe task PR-check artifact; preserving task state.` with exit 1.
The saved results report the completed endpoint absent and the other endpoints retained.
Direct inspection of retained files confirmed the completed metadata absent, the completed report unchanged, its backlog row closed, all four other metadata records and scratch files retained, the unsafe symlink and protected contents retained, and the unanswered input status unresolved.
The primary relayed the branch outcomes without performing cleanup itself.
It also reported that `fm_branch_processed` was unavailable under the driver's `--no-tools` primary configuration, so this was not a complete normal-primary acknowledgement test.
The cleanup log records guarded lab teardown, an unchanged default-session tripwire and exit 0.
These are historical observations, not a new passing gate run.

## Narrow authorization needed outside this phase

No supported branch-compatible marked-home setup exists in the inspected contract while these production overrides remain nonempty.
MAIN would need to authorize a separate compatibility change between production branch environment construction and the marked-lab capability contract, with containment tests preserving refusal of paths outside the lab.
This phase is explicitly forbidden to change either production behavior or the guard, remove safety variables, or relocate source to escape classification.
Stop here under the recorded decision rather than repeat a known blocked live launch.
After a separately authorized compatible setup exists, rerun the actual primary/branch scenarios using the named Herdr helper and combined cleanup trap, with the entire process tree in private namespaces.
No lint, formatter, static analysis, broad suite, pipeline control, publication or shared-infrastructure operation was performed.
