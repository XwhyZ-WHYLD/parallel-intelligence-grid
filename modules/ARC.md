# ARC — Adaptive Resilience & Compensation Layer

## Purpose

ARC (Adaptive Resilience & Compensation) is the **truth-preserving degradation layer**
of the Parallel Intelligence Grid.

ARC exists to ensure that **weak, noisy, partial, or degraded signal**
does not result in hallucination, collapse, or unsafe confidence amplification.

ARC does not increase intelligence.
ARC preserves **truth integrity, bounded confidence, and deterministic behavior**
when evidence quality degrades.

---

## Core Law

> **Signal amplification is allowed.  
> Evidence fabrication is forbidden.**

No output may exceed the strength of its evidence.

---

## Position in PIG Architecture

ARC sits **between the PIG Orchestrator and execution nodes**.


ARC governs:
- what may be amplified
- what must be suppressed
- when the system must abstain

---

## ARC Subsystems

### 1. SQI — Signal Quality Index (Truth Gate)

Every output must carry SQI metadata.

**SQI Components**

| Component | Meaning |
|--------|--------|
| Evidence Density (E) | Proofs, logs, grounding |
| Agreement Score (A) | Cross-node consistency |
| Drift Score (D) | Deviation from last stable truth |
| Uncertainty (U) | Entropy of inference |
| Freshness (F) | Temporal validity |
| Provenance (P) | Source trust |

**Normalized SQI Range:** `0.0 → 1.0`

**Gating Rules**

| SQI Range | Allowed Behavior |
|---------|----------------|
| 0.80 – 1.00 | Act |
| 0.55 – 0.79 | Suggest / conditional |
| 0.30 – 0.54 | Ask / gather evidence |
| < 0.30 | ZEP enforced (abstain) |

No SQI → no influence.

---

### 2. AGC — Adaptive Gain Control

AGC amplifies **signal visibility**, not certainty.

Rules:
- High-evidence features may be amplified
- High-variance features are suppressed
- Certainty language decays as SQI drops
- Confidence cannot exceed evidence
- Prediction budgets are capped

AGC = *visibility ↑, certainty ↔*

---

### 3. PCR — Predictive Completion (Labeled)

Prediction is allowed **only when explicitly labeled**.

Required output metadata:
- hypothesis list
- probability distribution
- missing evidence markers
- TTL (expiration)
- promotion requires new evidence

Prediction **cannot overwrite truth state**.

---

### 4. QWC — Quality Weighted Consensus

Consensus weight is not majority-based.


Rules:
- Majority alone is invalid
- High-impact actions require stronger quorum
- Trust decays on drift
- Local trust ≠ global trust

---

### 5. AIRS — Anomaly Isolation & Recovery

When a node behaves abnormally:
1. Quarantine
2. Challenge tests
3. Anchor comparison
4. Reintegration / isolation decision
5. Trust update

Prevents mesh poisoning and silent corruption.

---

### 6. Degradation Manager (Deterministic)

| Level | Condition | Behavior |
|-----|----------|---------|
| D0 | Stable | Full capability |
| D1 | Noisy | Denoise + AGC |
| D2 | Partitioned | Local truth + QWC |
| D3 | Severe | Fast path + abstain bias |
| D4 | No signal | ZEP only |

Transitions are deterministic.

---

### 7. ZEP — Zero Evidence Protocol

When SQI is below floor, the system may only output:
- known facts
- unknowns
- assumptions
- required evidence
- safest action

No guesses may be promoted to truth.

---

## Interaction With Other PIG Modules

- **PIG Core**  
  ARC enforces truth integrity before execution.

- **SPARC**  
  ARC informs *whether* execution is permitted.

- **PIG-IMMUNE**  
  ARC feeds degradation signals into immune governance.

- **EPR**  
  ARC prevents regeneration from amplifying corrupted signal.

- **TUNSYNC**  
  ARC governs cognition contraction during isolation.

ARC never escalates authority.

---

## Failure Modes ARC Prevents

- Weak-signal hallucination
- Confidence amplification under noise
- Majority-based false consensus
- Mesh poisoning
- Prediction masquerading as fact
- Silent drift during degradation

---

## Invariants Enforced by ARC

- Evidence bounds confidence
- Abstention is valid output
- Degradation is deterministic
- Prediction is labeled
- Trust decays faster than it grows
- No output exceeds SQI

If any invariant cannot be enforced,  
**ARC must force abstention.**

---

## Status

ARC is a **research construct**.

No implementation is provided.
No performance claims are made.
No production readiness is implied.

ARC defines *how intelligence must behave*
when signal integrity collapses.
