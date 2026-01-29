# START HERE — How to Read This Repository

This repository is not software.
It is not a framework you deploy.
It is not an implementation guide.

This is a **research-grade architectural canon** for governed,
failure-first, regenerative intelligence systems.

If this is your first time here, read in this order:

## Step 1 — Orientation
- README.md  
- MANIFESTO.md  

Understand *why this exists* and *what it refuses to become*.

## Step 2 — System Spine
- ARCHITECTURE.md  

This is the single source of truth.
All modules derive meaning from this document.

## Step 3 — Core Governance Logic
Read **one module at a time**:
- modules/PIG_CORE.md
- modules/SPARC.md
- modules/EPR.md

Do not skim. These are conceptual contracts, not feature lists.

## Step 4 — What Must Never Break
- invariants/CORE_INVARIANTS.md
- governance/REGENERATION_LEDGER.md

These define the safety envelope.

## Step 5 — Failure Is the Teacher
- threat-models/FAILURE_MODES.md
- threat-models/OFFLINE_DRIFT.md

This system is designed *for* failure, not in spite of it.

---

### Important Boundaries

- No code is provided intentionally
- No production claims are made
- No training or deployment guidance exists here

This repository answers **“how should intelligence behave under stress”**,
not “how to ship a model”.

If you are looking for APIs, this is not the place.
If you are designing resilient intelligence systems, welcome.
