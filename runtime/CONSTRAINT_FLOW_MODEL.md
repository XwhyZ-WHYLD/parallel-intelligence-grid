# Constraint Flow Model — PIG Reactor Mesh v1.0

This diagram shows how a single event/artifact moves through the Reactor Mesh constraint stack,
from ingress to output/tool/memory, including abstention, quarantine, and regeneration pathways.

```mermaid
flowchart TB

%% ---------- Ingress ----------
A[Ingress Event / Artifact<br/>User · Tool Output · Retrieval · Agent Msg · Sensor] --> B[BFL / Ingress Sentinel<br/>Schema + Normalization + Source Capsule]

%% ---------- Fast Deterministic Guards ----------
B --> C[FGT / Fast Guard & Throttle<br/>Rate limits · tool deny-routes · low-latency caps]
C --> D[PSC / Provenance & Signature Chain<br/>Identity · Signing · Hash lineage]

%% ---------- Evidence Packaging ----------
D --> E[EPK / Evidence Packaging Kernel<br/>Immutable evidence packet + replay id]

%% ---------- Behavioral & Epistemic Checks ----------
E --> F[IMMU / Behavioral Manipulation Detection<br/>Steering risk score + behavior vector]
E --> G[ARC / SQI Truth Gate<br/>Evidence density · drift · uncertainty · freshness]

%% ---------- Stability Governor ----------
F --> H[IMMUNE Core / Stability Regulator<br/>tolerance · hysteresis · anti-oscillation]
G --> H

%% ---------- Decision & Modes ----------
H --> I{SQI >= Act Threshold?}
I -- Yes --> J[SPARC / Execution Governance<br/>Permission gating · quorum windows · trace]
I -- No --> K{SQI >= Suggest Threshold?}
K -- Yes --> L[Conditional Output Mode<br/>suggestions + assumptions + TTL]
K -- No --> M[ZEP / Zero Evidence Protocol<br/>abstain + unknowns + required evidence]

%% ---------- Tool & Memory Controls ----------
J --> N{Tool Call Required?}
N -- Yes --> O[Tool Execution Firewall<br/>requires clean lineage + risk ok]
N -- No --> P[Output Packaging<br/>ECP schema + confidence bounds]

O --> Q{Memory Write?}
P --> Q
Q -- Yes --> R[Memory Write-Lock Gate<br/>block under risk/instability]
Q -- No --> S[Return Output to Orchestrator]

R --> S

%% ---------- Partition / Sync ----------
S --> T{Network State}
T -- Stable --> U[Normal Sync]
T -- Partitioned --> V[TUNSYNC / Partition Protocol<br/>signed packets + CRDT merge]
T -- Isolated --> W[Local-only truth domain<br/>no promotion to global truth]

%% ---------- Learning / Reinforcement ----------
U --> X{Learning Signal?}
V --> X
W --> X
X -- Yes --> Y[RIL / Integrity-Bound Reinforcement<br/>gated updates + rollbackable]
X -- No --> Z[No Learning]

Y --> Z

%% ---------- Recovery / Regeneration ----------
H --> AA{Instability / Thrash Detected?}
AA -- Yes --> AB[AIG / Autoimmune Governor<br/>cooldowns + freeze learning + rollback authority]
AB --> AC[EPR / Regenerative Recovery<br/>role reset + local healing + checkpoints]
AC --> S

%% ---------- Quarantine Path ----------
F --> AD{Risk >= Quarantine?}
AD -- Yes --> AE[QSB / Quarantine Sandbox<br/>isolate + replay + trace]
AE --> AF{Purge Required?}
AF -- Yes --> AG[Lineage Purge<br/>invalidate derived artifacts + caches]
AF -- No --> AH[Reintegrate with lowered trust]
AG --> AC
AH --> AC


---

## 2) Failure Propagation Map

Create: `runtime/FAILURE_PROPAGATION_MAP.md`

```md
# Failure Propagation Map — PIG Reactor Mesh v1.0

This map shows how major failure classes propagate through a mesh system, and the
specific module(s) responsible for containing each propagation path.

---

## A. Unbounded Execution / Tool Cascade

**Typical propagation**
1. Input triggers tool call
2. Tool output triggers more tool calls
3. Execution fans out across nodes
4. Costs + blast radius explode

**Containment**
- SPARC: permission gating + time-boxed quorum windows
- FGT: rate limits + tool deny-routes
- R-ORCH escalation ladder: observe → throttle → isolate
- Budgets: hard caps on tool calls and retries

**Residual risk**
- Misconfigured policies can permit “legal” runaway behavior

---

## B. Hallucination Cascade Under Weak Signal

**Typical propagation**
1. One node outputs weakly grounded claim
2. Other nodes treat it as fact
3. “Consensus” forms on fabricated state
4. Fabricated state becomes memory and is reused

**Containment**
- ARC/SQI: evidence proportionality + confidence gating
- ZEP: abstain when evidence below floor
- ECP schema: force evidence pointers + uncertainty markers
- Verifier node role in Reactor topology

**Residual risk**
- If evidence signals themselves are corrupted, SQI can be spoofed without provenance

---

## C. Behavioral Manipulation / Steering Drift

**Typical propagation**
1. Attacker injects subtle direction (urgency/authority/fear)
2. Model reasoning threshold shifts
3. Tool use becomes biased
4. Drift persists across memory + distributed updates

**Containment**
- IMMU: behavioral steering detector + invariance probe
- Pressure & anomaly guard: detects resource/timing pressure
- Memory write-lock: blocks persistence under elevated risk
- Distributed immune sharing: spreads abstract indicators
- ARC: prevents “high confidence” under low evidence

**Residual risk**
- Long-horizon slow drift can look like normal preference change without explicit baselines

---

## D. Autoimmune Collapse (System Attacks Itself)

**Typical propagation**
1. False positive triggers quarantine
2. Escalation ladder triggers again repeatedly
3. System enters thrash loop
4. Availability collapses despite no real attack

**Containment**
- IMMUNE Core: tolerance + hysteresis (avoid flip-flopping)
- AIG: anti-thrash invariant + cooldown + learning freeze
- R-ORCH two-key escalation rule
- Budget ceilings: block repeated resets

**Residual risk**
- Overly sensitive thresholds → chronic guarded mode

---

## E. Partition Collapse (Network Split → Divergent Truth)

**Typical propagation**
1. Mesh splits into partitions
2. Each partition evolves local state
3. Rejoin causes conflict storms
4. Wrong state wins or merges unpredictably

**Containment**
- TUNSYNC: partition-state transitions + signed packets
- CRDT merge logic for conflict-safe convergence
- “Local truth domains”: no promotion to global truth without reconciliation
- ARC: freshness + provenance in SQI (stale state penalized)

**Residual risk**
- Semantic conflicts can be hard even if data conflicts are merge-safe

---

## F. Learning Corruption / Poisoned Updates

**Typical propagation**
1. Feedback signal contaminated
2. Update accepted as reinforcement
3. System becomes confidently wrong
4. Corruption spreads via sharing

**Containment**
- RIL: gated learning acceptance + reversible updates
- Canary learning: limited scope testing first
- PSC/EPK: provenance + audit trails for learning events
- AIG: freeze learning when unstable

**Residual risk**
- If outcomes are hard to measure, “accuracy” feedback can be gamed

---

## G. Node Compromise / Malicious Peer

**Typical propagation**
1. Node outputs signed but misleading content
2. Peer trust remains high initially
3. Node poisons consensus + memory + sync packets

**Containment**
- AIRS / anomaly isolation: challenge tests + anchor comparison
- Trust decay: rises slowly, decays fast
- Quarantine sandbox + lineage purge
- Weighted consensus: SQI × trust × environment fit (majority alone invalid)

**Residual risk**
- Compromised keys undermine provenance unless hardware/attestation exists

---

## Summary Table

| Failure Class | Primary Containment | Secondary Containment |
|--------------|----------------------|------------------------|
| Unbounded execution | SPARC, FGT | Budgets, R-ORCH |
| Hallucination cascade | ARC/SQI, ZEP | ECP schema, Verifiers |
| Behavioral manipulation | IMMU | Memory lock, ARC |
| Autoimmune collapse | AIG, IMMUNE | Two-key escalation, budgets |
| Partition collapse | TUNSYNC | Local truth domains, ARC |
| Learning corruption | RIL | Canary learning, AIG freeze |
| Malicious peer | AIRS + Trust decay | Quarantine + purge |
