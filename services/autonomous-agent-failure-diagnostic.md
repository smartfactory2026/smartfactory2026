# Autonomous Agent Failure Diagnostic

## What this service is

A focused technical diagnostic for AI agents that **work sometimes, fail unpredictably, stall, waste actions/tokens, misuse tools, or improve in development but fail to transfer to real evaluation or production**.

The objective is not to replace your model by default.

The objective is to determine **where useful capability is being lost** and identify the smallest defensible intervention with the highest expected operational value.

---

## Problems this diagnostic is designed for

This service is useful when an AI agent:

- gets stuck in loops or keeps exploring after it already has enough information;
- performs well locally but degrades in benchmark, staging, or production conditions;
- fails inconsistently across repeated runs;
- uses too many actions, tokens, or tool calls;
- produces the right local action but maintains the wrong global world model;
- receives incomplete/stale tool feedback;
- suffers from runtime, scheduling, timeout, or contention effects;
- improves after a change, but the team cannot establish **why**;
- has accumulated many patches and experiments without a reliable failure taxonomy;
- needs an evidence-backed decision on whether to repair, redesign, or leave a subsystem unchanged.

---

## What you provide

Depending on the system, the diagnostic can work from a bounded set of materials such as:

- agent source or relevant modules;
- prompts / policies;
- traces or trajectories;
- tool-call logs;
- benchmark or evaluation results;
- failure examples;
- configuration/runtime information;
- before/after experiment outputs;
- known constraints and success criteria.

The minimum required evidence is agreed before analysis.

Sensitive customer material is not published as part of the public case-study portfolio.

---

## Diagnostic framework

The investigation separates common failure layers instead of treating every bad outcome as a model problem.

### 1. Perception / observation
Did the agent receive and interpret the relevant state correctly?

### 2. Feedback fidelity
Did the agent receive a complete and current account of what its previous action actually changed?

### 3. World-model integration
Did the agent integrate correct local evidence into the correct global model?

### 4. Decision / commitment policy
Did it keep probing when it should have acted, or commit before enough evidence existed?

### 5. Tool / runtime layer
Did tool errors, timeouts, retries, queues, concurrency, or infrastructure distort behavior?

### 6. Memory / context
Was relevant information unavailable, stale, duplicated, or overwhelmed by low-value context?

### 7. Evaluation / transfer
Is the apparent improvement real, or is it caused by selection effects, leakage, stochastic variance, or a difference between development and deployment conditions?

---

## Deliverables

A standard diagnostic produces:

### Failure Map
A structured taxonomy of observed failure modes with evidence references.

### Evidence Ledger
Clear separation between:
- observation;
- inference;
- hypothesis;
- verified result;
- unknown.

### Root-Cause Candidates
Ranked hypotheses with supporting and contradicting evidence.

### Minimal Experiment Plan
The smallest set of controlled tests capable of distinguishing the highest-value hypotheses.

### Repair Recommendation
A bounded recommendation that distinguishes:
- repair existing capability;
- change control policy;
- change runtime/harness;
- improve observability;
- re-evaluate the model;
- or make no change because the evidence does not justify one.

### Claim Ceiling
An explicit statement of what the available evidence proves — and what it does not.

---

## Optional implementation phase

After the diagnostic, a separate engagement can cover:

- minimal repair implementation;
- regression tests;
- reproduction / qualification;
- before/after measurement;
- deployment-readiness evidence;
- ongoing reliability monitoring.

The diagnostic does not automatically commit the client to implementation.

---

## What makes the approach different

The process is built around several engineering rules:

**Diagnose before rebuilding.**

**Evidence over assertion.**

**Development improvement is not deployment transfer.**

**Artifact reproducibility is not the same as outcome reproducibility.**

**Preserve negative results so the team does not pay twice for the same failed idea.**

**Prefer one small causal delta over many simultaneous changes.**

---

## Public evidence

The methodology is informed by work performed during ARC-AGI-3 2026.

A public case study is available here:

[ARC-AGI-3 2026 — Agent Diagnostics Case Study](../case-studies/arc-agi-3-agent-diagnostics.md)

Verified V8 public leaderboard score: **30.96**.

That score is used as evidence of a real working competition system, not as proof that any single diagnostic mechanism caused the result.

---

## Confidentiality boundary

Client work and private technical material are confidential by default.

A public case study is created only from material that is already public or explicitly approved for disclosure.

No private Smart Factory implementation is required to be shared with the client or published.

---

## Best fit

This service is best suited to:

- AI-agent startups;
- research teams;
- companies building tool-using LLM agents;
- benchmark / evaluation teams;
- workflow-automation systems;
- engineering teams with expensive agent failures;
- teams that need a defensible technical answer before investing in a rewrite.

---

## Engagement path

**1. Diagnostic**  
Establish the failure surface and evidence.

**2. Controlled verification**  
Test the highest-value hypotheses.

**3. Minimal repair**  
Implement only the justified delta.

**4. Qualification**  
Measure whether the repair survives regression and realistic conditions.

**5. Ongoing support**  
Optional periodic analysis for new failures or system changes.

---

## Start

If you have an AI agent that works inconsistently, stalls, wastes resources, or behaves differently in production than in development, contact me through my GitHub profile with a short description of:

- what the agent is intended to do;
- what failure you observe;
- what evidence/logs you already have;
- what outcome would make the diagnostic valuable.

Initial discussion can determine whether the problem is a good fit before any deeper technical work begins.
