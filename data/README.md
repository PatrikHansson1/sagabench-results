<!-- DRAFT — internal until the chairman approves publication. -->

# data/ — aggregate result files (scores only)

These files carry the replicate score sets and derived results behind the paper's findings. They are **verbatim copies** of the research working files (filenames preserved, including dates) — nothing reformatted, nothing recomputed.

**Honesty note on replayability:** unlike `../replays/`, most files here record *composite scores per replicate*, not the underlying edict-logs. The per-run replay packages for these replicate sets live in the research archive and are exported to this repository batch-by-batch as they are curated. An aggregate file being present here does NOT yet mean every one of its runs has a downloadable replay package. The paper's rule stands: a published number whose replay package cannot be produced on request is void.

| File | What it is |
|---|---|
| `B1-RESULTS-2026-07-23.json` | Full 15-model sweep (135 cells), single run per cell — the alpha leaderboard's raw material. Single run = *unresolved*, per the reading rules. |
| `B2-VB2-RESULTS-2026-07-23.json` | The VB2-matched panel used for the H2 validity test. |
| `H2-RESULTS-2026-07-23.json` | H2 confirmatory result: SagaBench vs economic-agency benchmark, ρ ≈ −0.046 (null, published as such). |
| `B3-FRONTIER-TAILS-240181.json` | N=5 replicate sets on knife-edge seed 240181 (opus-4-8, deepseek, gpt-4o, gpt-5.6-terra, haiku, sonnet-5) — the replicated-tail finding. |
| `KE2-RESULTS-520377.json` | Pre-registered second knife-edge (520377), N=5 × 4 models — pre-reg verdict MIXED, reported per the locked rule. |
| `KE3-RESERVE-550398.json` | Pre-registered reserve knife-edge (550398): 0 extinctions across all 4 models — the tail requires a genuinely fragile world. |
| `B9-TAIL-GENERALIZATION.json` | Seed-specificity check: 0 extinctions on 440321/200153 vs 5/20 on 240181. |
| `B10-CROSS-HORIZON-RELIABILITY.json` | Single-run noise and ICC by horizon — why replication is the measurement. |
| `CEILINGS-PRESERVATION.json` | Engineered-ceiling search results (preservation seeds); provisional lower bounds. |
| `CEILINGS-240181-DEEPSEARCH-2026-07-24.json` | Deep search on 240181: ceiling 100 → 118; best move is restraint (TEMPER_AMBITION@25). |
| `LEADERBOARD-2026-07-23.json` | The published leaderboard snapshot (23 models, 4 vendors) with reliability profiles. |

All scores are counterfactual Δ composites on engine `4f237acf…` with preregistered weights. Read the paper's §6 before quoting any single number — the profiles, not the podium, are the story.
