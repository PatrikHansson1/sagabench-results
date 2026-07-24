<!-- DRAFT — internal until the chairman approves publication. Adapted from VERIFICATION-PROTOCOL.md v1.0 (60-EXIT-READINESS). -->

# Verifying a SagaBench result

*For engineers. Purpose: demonstrate that any SagaBench result is a mathematical fact you can check on your own hardware — not a claim you must trust.*

## 1. The guarantee

A SagaBench run is fully specified by the **replay package**:

```json
{ "engineSha": "<SHA-256 of the engine file>",
  "seed":      <uint32>,
  "founders":  <object | null>,
  "ticks":     <int>,
  "edicts":    [ { "year": <int>, "type": "<EDICT>", "args": { ... } }, ... ] }
```

**Claim:** given this package, the entire world history — every event, every agent's state, every tile, serialized with each number as its exact 64-bit IEEE-754 bit pattern — is reproduced **bit-for-bit**, on Node.js, in a browser (V8), or on .NET (Jint). Two runs match if and only if every value is bit-identical. Equality is checked as SHA-256 over the canonical serialization.

Why this holds: the simulation's only randomness source is a seeded mulberry32 PRNG (no `Math.random`, no wall clock, no external I/O); the steward layer injects edicts as deterministic state transitions at year boundaries and never consumes simulation randomness; presentation-layer variety derives from position hashes outside the simulation stream. One known cross-host hazard — `Math.hypot` differing by 1 ULP between JS engines and .NET — is neutralized by loading a shared prelude that pins one algorithm before the engine loads.

## 2. Verify in five steps (≈2 minutes, Node ≥ 18, no dependencies)

1. **Obtain the verification build** (`emergence-engine-<version>.js`, eval-only license) plus `harness/prelude-hypot.js`, `harness/harness.js`, `saga-steward.js`, and the published golden/canon files. <!-- [GATED: distribution channel — GATED-DECISIONS.md §1] -->
2. **Check the engine bytes:** `sha256sum emergence-engine-<version>.js` must equal `engineSha` from the replay package. If not, stop — you have the wrong build.
3. **Replay:** load, in order, prelude → engine → harness → steward into one JS context; call `SagaSteward.runSteward(seed, ticks, edicts, founders)`.
4. **Canonicalize & hash:** `sha256( EmergenceGolden.canonicalize(result.payload) )`.
5. **Compare** with the published run hash. Equal ⇒ you have reproduced the exact history, and every derived score follows arithmetically. Not equal ⇒ our claim is falsified — please tell us.

Reference runner: `run-standalone.js golden` performs steps 2–5 against the engine's own golden masters and prints GREEN/RED per seed; it is the same machinery, pointed at baseline worlds.

## 3. What this makes impossible

- **Cherry-picking:** a leaderboard entry without a working replay package is, by our own rules, void.
- **Judge ambiguity:** scores are closed-form functions of the replayed history (counterfactual delta vs. the same seed with an empty edict log) — there is no learned judge model to second-guess.
- **Environment drift:** the engine file is frozen per version and hash-locked; scores are never compared across engine versions. Golden masters re-verify the build on every CI run.
- **Contamination:** worlds are procedurally generated from seeds; hidden evaluation seeds are disclosed (deposited publicly) only after rotation out of use.

## 4. Scope and honesty notes

The *world* is exactly reproducible from the decision log. The *policy* that produced the log (e.g., an LLM) may not be re-generatable — the replay packages in this repository therefore include complete prompts/transcripts per run, so the scoring chain is auditable end-to-end even where generation is not repeatable. Cross-runtime equality is continuously verified on Node and V8; the Jint/.NET path was golden-verified on engine 2.3.x and is re-verified per release.

*This protocol is versioned; changes are logged in this repository.*
