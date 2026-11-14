# Process notes — analysis integrity

Lessons about *how to run the analysis reliably*, surfaced during corpus building. These are not
design principles; they protect the quality of the design principles.

## Integrity rules for source analysis

- **Validate the source identifier before fan-out.** Confirm the file is readable (a screenshot
  or page list returns) before dispatching layer agents. A placeholder/invalid key must
  **halt-and-report with zero findings**, never trigger a fallback "read from memory" path.
- **Never back-fill a required output.** If an agent cannot observe the file, it must say so and
  return empty — not restate existing corpus knowledge as if freshly observed. Fabricated
  confirmation is worse than a missing source.
- **Confidence-label coherence check.** If sibling layers on the same file report wildly different
  confidence (one "high", one "blocked/low"), distrust the "high" — it is likely re-abstraction,
  not observation. Downgrade it.
- **Cached-artifact provenance check.** Match a scratchpad artifact's canvas id/name/key to the
  intended target before trusting it as that target's data.
- **Candidate quarantine.** Reasonable-but-unobserved principles from a blocked run are logged as
  **candidates**, never promoted into the validation ledger or allowed to raise a tier, until a
  *readable* source observes them.

## Applied history

- **Source 08 (first run):** 3 of 5 layer agents hit read-blocks; findings were a mix of real
  observation and re-abstraction. Per the rules above, that run was **not integrated** as
  validated method. Its genuinely-new candidates (register-selection as explicit Step 0;
  register-scaled semantic-matrix cardinality; accessibility obligation relocates to selection-time
  when adopting a utility palette; in-grid cell interruption; dark-band punctuation) are held as
  **candidates pending a clean re-run**. The file was confirmed readable afterward, so Source 08
  was re-run fresh.

## Ledger rule: a void/halted source is confirmation-neutral

A source that produced zero observations (invalid key, unreadable frames) must not touch the
VALIDATION ledger — it neither confirms nor weakens any principle. **Confidence tiers move only on
independent observation.** Record the void for provenance, with zero ledger weight. This governs
what the *integrator* does with a compliant-but-empty run (distinct from the agent-side rule
"never restate prior corpus as freshly observed").

## Orchestration: pass concrete values, not lazy `args` indirection

Two Source-08 runs failed because the workflow's `args.fileKey` arrived as the string
`"undefined"` — `args` did not propagate on those invocations. Every agent correctly halted. Fix
applied: for a single high-stakes source, hardcode the fileKey/targets in a dedicated script
rather than relying on `args`. For parameterized runs, validate the key against
`^[0-9a-zA-Z]{22,128}$` at the orchestrator before fan-out, so one bad input fails fast instead of
burning N parallel agents.
