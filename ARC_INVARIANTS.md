# ARC Invariants — Adaptive Resilience & Compensation Layer

These invariants define the **non-negotiable safety and truth constraints** of the ARC
(Adaptive Resilience & Compensation) layer within the Parallel Intelligence Grid (PIG).

ARC exists to preserve **truthful operation under degradation**.
It must never increase confidence beyond evidence, nor trade integrity for availability.

If any invariant cannot be satisfied, ARC **must abstain**.

---

## Invariant ARC-1: Evidence Bounds All Output

No output may express confidence, certainty, or authority greater than the strength
of its supporting evidence.

- Signal amplification is permitted  
- Evidence fabrication is forbidden  

If evidence quality decreases, confidence **must decrease or hold**, never increase.

---

## Invariant ARC-2: SQI Is Mandatory for Influence

Every output passing through ARC **must carry Signal Quality Index (SQI) metadata**.

If SQI is missing, corrupted, or unverifiable:
- The output has **zero influence**
- ZEP (Zero Evidence Protocol) is enforced

No SQI → no action → no exception.

---

## Invariant ARC-3: Degradation Is Deterministic

For a given degradation level, ARC behavior must be:

- Predictable
- Repeatable
- Non-adaptive in unsafe directions

ARC may reduce capability, scope, or expressiveness,
but it must never improvise new behavior under stress.

---

## Invariant ARC-4: Prediction Must Be Explicitly Labeled

All predictive or inferential outputs must be clearly marked as:

- hypothesis
- estimate
- assumption
- projection

Predictions must include:
- probability bounds
- missing evidence markers
- time-to-live (TTL)

Unlabeled prediction is treated as **fabrication**.

---

## Invariant ARC-5: Abstention Is a Valid Outcome

ARC must allow and preserve **intentional silence**.

When evidence is insufficient:
- Withholding output is preferred
- Declaring “unknown” is correct
- Refusal is compliant behavior

Availability pressure must never override epistemic integrity.

---

## Invariant ARC-6: Trust Decays Faster Than It Accrues

Trust scores must:

- Increase slowly
- Decay rapidly under drift, anomaly, or failure
- Never self-repair without evidence

This prevents confidence runaway, feedback loops, and trust inflation.

---

## Invariant ARC-7: ARC Cannot Escalate Authority

ARC may:
- modulate
- attenuate
- gate
- abstain

ARC may not:
- override governance (SPARC)
- modify objectives (PIG Orchestrator)
- initiate regeneration (EPR)
- redefine policy or truth

ARC is a **compensation layer**, not a decision authority.

---

## Invariant ARC-8: Zero Evidence Defaults to ZEP

When SQI falls below the minimum threshold:

- ARC must enforce Zero Evidence Protocol (ZEP)
- Outputs are limited to:
  - known facts
  - declared unknowns
  - assumptions
  - required evidence
  - safest available action

Guessing is never permitted, regardless of pressure or urgency.

---

## Failure Handling Rule

If ARC invariants conflict with:
- performance
- latency
- availability
- user expectation
- system demand

ARC must choose **invariant preservation** and degrade or abstain.

---

## Status

These invariants are **architectural constraints**, not implementation guidance.

They define:
- what ARC is allowed to do
- what ARC must never do
- how truth survives degradation

No production readiness is implied.
No optimization claims are made.
