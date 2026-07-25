<!-- DRAFT — internal until the chairman approves publication (G2/repo gate). Prepared by the CEO 2026-07-24. Nothing in this folder has been pushed anywhere. -->

# SagaBench — Published Results & Replay Packages

**SagaBench** is Long-Horizon Agentic Evaluation: bit-reproducible civilization simulations that measure what a single run cannot — reliability and tail-risk over decades of simulated time. This repository contains the published results behind the paper *"The Steward's Paradox: Capable AI Agents Can End Civilizations That Survive Without Them"* and the replay packages that let you verify them on your own hardware.

**Status: v0.1 ALPHA.** Small N, evolving coverage. Every number carries its N; nothing here is a safety claim.

## The one promise this repo exists to keep

You do not have to trust us. A SagaBench run is fully specified by its **replay package** — an `(engineSha, seed, edict-log)` triple. Feed that triple to the hash-locked engine build and the entire simulated history reconstructs **bit-for-bit** (IEEE-754 exact, verified across three runtimes). Every derived score follows arithmetically. If a published number does not replay, it is — by our own published rule — void, and we retract it.

See **[VERIFYING.md](VERIFYING.md)** for the five-step procedure (≈2 minutes, Node ≥ 18, no dependencies).

## What is in this repository

| Folder | Contents | Replayable? |
|---|---|---|
| `replays/` | Complete replay packages — config, `(engineSha, seed, edict-log)`, per-layer scores, and the full model transcript (prompts + responses) for end-to-end auditability | **Yes — bit-for-bit** |
| `data/` | Aggregate result files behind the paper's findings (replicate score sets, leaderboard, pre-registered outcomes, engineered-ceiling searches) | Scores only — see `data/README.md` |
| `MANIFEST.json` | SHA-256 of every file in this repository | — |

Naming: `replays/<model>_<task>_<seed>.json`. Tasks: `crisis` (20y), `development` (60y), `preservation` (120y).

## What is deliberately NOT here — and why results are still verifiable

The **world-generator, the knife-edge screening pipeline, and the hidden holdout seeds** are not disclosed; they are what keeps future evaluations unspoiled. Verification does not require them: published and public-world results replay directly from the packages in this repo, and hidden-world results (Private Seasons) run through a **sealed verifier** that confirms a replay without revealing the seed. Retired evaluation seeds are deposited publicly after rotation out of use, so our past remains auditable.

The **verification engine build** (`emergence-engine-<version>.js`, eval-only license) and its harness are distributed per VERIFYING.md step 1. <!-- [GATED: exact distribution channel — see GATED-DECISIONS.md §1] -->

## How to read the numbers

- Scores are **counterfactual**: Δ = V(world | steward) − V(world | agentless), same seed, preregistered weights. A good outcome can be luck; Δ measures the agent's causal contribution.
- **One run is an anecdote.** Replicate sets are the measurement; the tails are the finding. Entries without replicates are *single run · unresolved* — which is not the same as "no tail detected."
- A zero-catastrophe result is reported as **"no catastrophic tail detected at N"** — never "safe."

## Found a discrepancy?

If a replay does not reproduce a published hash or score, that falsifies our claim — please open an issue. That is the standard we asked to be held to.

---
*SagaBench AB · [sagabench.com](https://sagabench.com) · contact info@sagabench.com · repository github.com/PatrikHansson1/sagabench-results. Independent research. Not affiliated with, or endorsed by, any of the labs whose models appear in these results. Engine build for all results in this repo: `engineSha 4f237acf…` (full hash in each package).*
