# ARC-AGI-3 2026 — Agent Diagnostics Case Study

## Executive summary

This case study documents a bounded investigation of **when an interactive AI agent should stop probing and commit to action**.

The work was performed in the ARC-AGI-3 2026 setting, an interactive reasoning benchmark in which agents must explore unfamiliar environments, infer goals and mechanics, build working world models, and act efficiently.

**Verified official public result:** V8 scored **30.96** on the ARC-AGI-3 public leaderboard.

- Submission reference: `57455070`
- Frozen V8 source SHA-256:  
  `3D386D2023A269C4690E75B8A129A05063DC957F265FBD637E63EDCFC73A3926`
- Public release notebook: `adilblabs/arc3-v8-public-release-57455070`
- Final private score / final competition placement: **unknown pending organizer results**

This document does **not** claim that one intervention caused the 30.96 official score.

---

## The engineering question

Interactive agents repeatedly face a control decision:

> Should the agent keep probing for more information, or does it already know enough to commit to an action sequence?

More probing can improve the working model of the environment, but it consumes actions and time. Committing can turn sufficient understanding into progress, but premature commitment can lock the agent into a bad hypothesis.

The useful question is therefore not:

> “Is more reasoning always better?”

It is:

> **“When does additional information have enough decision value to justify its cost?”**

---

## System context

The submitted system inherits a public ARC-AGI-3 agent stack built around the Duck/TAAF harness and public model/runtime components.

The project contribution studied here is **not** a claim of inventing the underlying harness or the public commitment mechanism.

The evaluation focused on:

- exact source / result provenance;
- agent failure diagnosis;
- probe-versus-commit behavior;
- completion versus action cost;
- generalization checks;
- negative-result preservation;
- separating development evidence from official competition evidence.

---

## Evidence hierarchy

The project deliberately separates different evidence classes.

### Official competition evidence

**V8**
- public score: **30.96**
- official submission ref: `57455070`

**Exact-source V8 replication**
- public score: **26.27**

The source artifact was reproduced exactly, but the score was not.

This gives an important engineering lesson:

> **Artifact reproducibility does not imply stochastic outcome reproducibility.**

### Development intervention evidence

A targeted comparison was run on three preselected public games with repeated passes.

Treatment:
- completed **72 / 72** levels;
- completed **12 / 12** repeated runs.

Control:
- completed **67 / 72** levels;
- completed **8 / 12** repeated runs.

Across the repeated game/pass pairs:
- mean score difference: **+4.98**
- median difference: **0**
- treatment used **398 more actions**

These repeated passes are **not 12 independent experimental units**. The primary independent unit is the game, so this is bounded development evidence rather than randomized population-level causal proof.

### Broader descriptive transfer

A separate one-pass treatment run across 25 public games produced:

- mean score: **61.15**
- wins: **12 / 25**
- levels completed: **138 / 183**

Relative to each game's historical four-pass control distribution, treatment exceeded:
- control mean in **17 / 25** games;
- control median in **15 / 25** games;
- all four control passes in **9 / 25** games;
- and was below all four control passes in **0 / 25** games.

This is useful descriptive corroboration, not a randomized 25-game causal estimate.

---

## What the evidence suggests

The strongest supported interpretation is a **completion-headroom hypothesis**.

Commitment guidance appears most useful when:

1. the agent has learned enough of the environment mechanics to act;
2. genuine completion headroom remains;
3. continued probing risks stalling rather than materially changing the decision.

When completion is already saturated, additional actions can instead reduce efficiency.

That means intervention value is **state-dependent**, not monotonic.

---

## What did not generalize cleanly

Negative evidence is part of the result.

A later variant increased local analyzer context by 8,192 tokens but scored **28.50** officially.

A separate development candidate reached strong local development performance but did not improve the official result.

These observations reinforce a rule that applies far beyond ARC-AGI-3:

> **Local improvement is not the same thing as deployment transfer.**

Before attributing performance to a code delta, the experiment must separate:

- source identity;
- runtime environment;
- stochastic variation;
- systems pressure;
- environment distribution;
- the intervention itself.

---

## Engineering lessons

### 1. Diagnose before rebuilding

When an agent underperforms, replacing the model or adding more memory is not automatically the right answer.

First identify whether the dominant problem is:

- perception;
- feedback fidelity;
- world-model integration;
- tool/runtime failure;
- scheduling / resource pressure;
- decision policy;
- premature or delayed commitment.

### 2. Small control deltas can matter

The useful intervention may be a small policy or harness change rather than a larger model.

### 3. Preserve negative results

Failed hypotheses prevent repeated engineering spend.

### 4. Evidence classes must stay separate

`DEVELOPMENT_RESULT != OFFICIAL_RESULT != CAUSAL_PROOF != HYPOTHESIS`

### 5. Reproducibility needs two layers

- **artifact reproducibility** — same source/configuration;
- **outcome reproducibility** — statistically stable behavior/results.

They are related, but they are not equivalent.

---

## Commercial relevance

The same diagnostic discipline applies to production AI-agent systems.

An underperforming agent may not need a new foundation model. It may need a disciplined investigation of where useful capability is lost between observation, reasoning, tools, memory, scheduling, and action.

### Autonomous Agent Failure Diagnostic

A typical engagement can produce:

- behavioral failure taxonomy;
- trace / trajectory analysis;
- evidence-bound root-cause hypotheses;
- controlled comparison plan;
- generalization and regression checks;
- minimal repair recommendation;
- before/after evidence report;
- explicit limits on what the evidence proves.

The objective is to find the **smallest defensible change with the highest expected operational value**.

---

## Attribution and disclosure boundary

The ARC-AGI-3 system uses inherited/public work and third-party components. Credit and upstream licensing must remain explicit.

Relevant lineages include:

- Tufa Labs / Duck / TAAF;
- Daniel Franzen's public ARC-AGI-3 work;
- Qwen model lineage;
- Albucino / RadixArk draft-model lineage;
- SGLang / Pennyroyal runtime lineage;
- Intel AutoRound.

This case study does not claim authorship of inherited mechanisms.

Private Smart Factory architecture, unrelated product code, internal governance, reusable private capability infrastructure, credentials, and nonessential forensic material are intentionally outside this public case-study boundary.

---

## Current status

ARC Prize 2026 has closed submissions.

The V8 **30.96 public score is verified**. Final private score and final competition placement remain unknown until the organizers publish the final results.

This page will be updated only when newer authoritative evidence is available.
