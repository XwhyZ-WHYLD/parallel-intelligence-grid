# Minimal Simulation Proposal — PIG Reactor Mesh v1.0

Goal: produce credible, measurable evidence that the Reactor Mesh constraint stack
reduces failure under adversarial, noisy, and partitioned conditions — without requiring a full implementation.

This is an implementation-neutral simulation blueprint.

---

## 1. Simulation Objectives

Measure whether constraint enforcement improves:

1) Truth integrity under weak signal  
2) Resilience under partition and rejoin  
3) Resistance to behavioral steering  
4) Stability (avoid autoimmune thrash)  
5) Recovery (local regeneration vs restart)  
6) Learning integrity (avoid poisoned reinforcement)

---

## 2. Simulation Environment (Abstracted)

### Entities
- **Nodes**: N ∈ {5, 20, 100}
  - Types: Anchor, Worker, Verifier, Vault, Cache
- **Events**: inputs arriving over time
- **Network**: graph with variable connectivity & latency
- **Artifacts**: message packets, tool outputs, memory writes, sync packets

### Conditions
- Normal
- Noisy (signal variance ↑)
- Partitioned (graph splits)
- Isolated (single node)
- Adversarial (steering + poisoning attempts)

---

## 3. Two Configurations to Compare

### Baseline System (Control)
- Parallel inference + simple majority
- No SQI gating
- Minimal provenance
- Retries instead of EPR
- No immune / anti-thrash protection
- Sync without signed packets / conflict control

### Reactor Mesh System (Treatment)
- SPARC gating
- ARC/SQI + ZEP abstention
- IMMU steering detection
- IMMUNE + AIG stability control
- EPR local regeneration + checkpoints
- TUNSYNC signed packets + CRDT merge
- RIL gated learning acceptance

---

## 4. Metrics (Must-Haves)

### Integrity Metrics
- **Hallucination Rate (HR)**: % of outputs later proven unsupported
- **Evidence Alignment (EA)**: % outputs with valid evidence pointers
- **Overconfidence Index (OCI)**: confidence minus evidence strength

### Resilience Metrics
- **Uptime Utility (UU)**: useful outputs per time unit under degradation
- **Partition Survival (PS)**: utility retained during partition
- **Rejoin Coherence Time (RCT)**: time to converge after reconnection

### Security Metrics
- **Steering Success Rate (SSR)**: % attacks that shift action selection
- **Poison Spread Factor (PSF)**: how many nodes accept contaminated state

### Stability Metrics
- **Thrash Index (TI)**: oscillation between modes per hour
- **False Positive Cost (FPC)**: quarantines triggered with no true attack

### Recovery Metrics
- **Recovery Latency (RL)**: time from failure to stable operation
- **Restart Avoidance Rate (RAR)**: % recoveries without global reset

### Learning Metrics
- **Poison Acceptance Rate (PAR)**: poisoned updates accepted
- **Rollback Success (RS)**: % of rollbacks restoring integrity

---

## 5. Attack & Failure Scenarios

Run each scenario with identical seeds for control vs treatment.

### Scenario A: Weak signal hallucination
- Evidence quality drops gradually
- Baseline tends to fabricate completion
- Reactor Mesh should shift to conditional + ZEP

### Scenario B: Behavioral steering campaign
- Inject urgency + authority + repeated direction
- IMMU should increase risk, block memory/tool writes

### Scenario C: Partition + rejoin conflict storm
- Split network into 2–3 partitions
- Divergent local truth emerges
- TUNSYNC should preserve local domains, reconcile safely

### Scenario D: Autoimmune overreaction
- Benign noise triggers false positives
- Treatment should dampen with IMMUNE + AIG cooldown

### Scenario E: Poisoned reinforcement
- Provide corrupted feedback
- RIL should canary + reject or rollback

---

## 6. Minimal Implementation Approach (Simulation-Only)

You do NOT need real LLM calls.

Represent node outputs as:
- claim vectors
- evidence flags
- confidence numbers
- drift scores
- provenance weights

“Truth” can be defined by a hidden ground-truth generator for each task.

Steering attacks can be modeled as bias shifts in action selection thresholds.

---

## 7. Success Criteria (Pass/Fail)

The Reactor Mesh “wins” if it achieves:

- ≥50% reduction in hallucination rate under weak signal
- ≥50% reduction in steering success rate
- ≥30% reduction in thrash index
- ≥30% faster rejoin coherence time
- ≤15% false positive cost increase (trade-off tolerance)
- ≥40% reduction in poison acceptance rate

---

## 8. Deliverables (What You Publish)

- Simulation spec (this doc)
- Reproducible parameter table (N, latency, partition rate, attack rate)
- Results plots (even synthetic)
- A short “Limitations” section
- Clear mapping: which module reduced which metric

This becomes evidence for:
- arXiv preprint
- serious GitHub credibility
- investor diligence narratives
