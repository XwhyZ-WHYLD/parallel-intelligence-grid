## What This Diagram Represents

This diagram describes the baseline survival architecture of PIG when operating
in noisy, adversarial, or partially disconnected environments.

It models how inputs are filtered, how threats are escalated without panic,
and how the system prevents autoimmune collapse while preserving operation.

---

## Why This Exists (Failure Mode It Solves)

Without this structure:
- False positives trigger runaway shutdowns
- Learning systems overreact to noise
- Recovery attempts amplify damage
- Offline operation causes silent drift

This architecture assumes contamination is normal and designs for endurance,
not purity.

---

## How To Read This Diagram (Top → Bottom)

1. **Boundary Filter Layer (BFL)**  
   Normalizes and classifies all inputs. Unknowns are routed safely, not rejected.

2. **Fast Guard & Throttle (FGT)**  
   Deterministic, <5ms controls. No learned system may override this layer.

3. **Provenance & Signature Chain (PSC)**  
   Every action, tool, and output is signed. Unsigned entities cannot escalate.

4. **Evidence Packaging Kernel (EPK)**  
   Suspicious behavior is converted into immutable evidence packets.

5. **Response Orchestrator (R-ORCH)**  
   Enforces stepwise escalation with multi-signal confirmation.

6. **Autoimmune Governor (AIG)**  
   Overrides the entire system if thrashing or instability is detected.

7. **EPR Regeneration Engine**  
   Repairs invariant violations and resumes operation without full restart.

---

## Invariants Enforced By This Diagram

- No single signal may trigger escalation
- No learning is irreversible
- Availability never overrides integrity
- Recovery is bounded and auditable
- Silence is allowed when confidence is low
