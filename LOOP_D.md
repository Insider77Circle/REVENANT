# LOOP_D.md — Active Counter-Emulation & Peer Neutralization Specification

**Status:** Theoretical Architecture / Draft Contract  
**Overlay:** MACR (MUSE Adaptive Cognitive Runtime) — Exorcist Module  
**Parent Contract:** `RSI.md` (Extends Loops A, B, and C)

---

## Overview

While **Loop A** adapts within a single task, **Loop B** records cross-task shadow lessons, and **Loop C** evolves the harness offline via clean-room fork analysis, **Loop D** governs real-time, peer-to-peer counter-emulation. 

Loop D enables a REVENANT-augmented ARTEX deployment to detect, attribute, and neutralize hostile, unguarded ARTEX variants operating within an authorized perimeter or lab environment. It operates by deploying ephemeral, specialized subagent swarms controlled by the **JEV Governor**, prioritizing cognitive containment and resource exhaustion over destructive host-level actions.

---

## Architecture & Directory Mapping

Loop D integrates directly into the existing REVENANT Go codebase without altering immutable core surfaces:

* **`scout-hunter/` (Active Reconnaissance Swarm):** Ephemeral subagents that monitor network telemetry and local interfaces for behavioral signatures matching known ARTEX forks (e.g., `norma/0.4` HTTP headers, characteristic multi-LLM API burst patterns, exposed `mcphttp/` ports).
* **`guard/` (JEV Governor Gatekeeper):** Enforces target verification thresholds and authorization boundaries before any counter-subagent is permitted to transition from passive observation to active engagement.
* **`intercept/` & `traffic/` (Containment & Neutralization Engine):** Spawns specialized subagent roles (Illusionists, Tarpits, Sanitizers, Disruptors) to engage verified rogue instances.
* **`llmpool/` (Asymmetric Inference Allocator):** Manages token budgets for defensive subagents, ensuring high-efficiency decoy generation that forces disproportionate token expenditure on the hostile node.
* **`evidence/` & `archivestore/` (Cryptographic Audit & Delta Capture):** Logs hash-chained engagement receipts and extracts novel adversary behaviors for offline ingestion by Loop C's **Scout** and **Builder**.

---

## Subagent Swarm Taxonomy

Once the JEV Governor approves an engagement, Loop D orchestrates four distinct subagent archetypes:

| Subagent Role | Target Surface | Mechanism of Action |
| :--- | :--- | :--- |
| **Illusionist** | Exploration Graph / Memory | Injects high-entropy, synthetic network topologies and false-positive vulnerabilities into the adversary's observation stream, trapping its planning loop in recursive validation states. |
| **Tarpit** | `llmpool` / Inference Engine | Engages hostile subagents with deeply nested, computationally expensive reasoning traps (e.g., complex cryptographic puzzles or labyrinthine mock file systems) to exhaust the attacker's API credits and rate limits. |
| **Sanitizer** | Context Window / Prompt Layer | Leverages known weaknesses in guardrail-stripped forks by embedding defensive control sequences within simulated service banners, inducing state dumps or graceful task termination. |
| **Disruptor** | `egress/` & State Sync | Identifies and sinks the rogue instance's external telemetry, PostgreSQL state-sync channels, or compromised API key pools within the authorized boundary. |

---

## The Loop D Contract (Rules 9–14)

Loop D inherits all eight foundational rules of `RSI.md` (including *Immutable Surfaces*, *Flag Off by Default*, and *Clean-Room Only*) and introduces six binding operational constraints:

### 9. Multi-Signature Target Verification Gate
Counter-subagents **must not** engage any host or process based on a single indicator. Active containment requires cryptographic confirmation by the JEV Governor of **at least three (3) independent behavioral signatures** cross-referenced against the REVENANT Capsule Registry.

### 10. Non-Destructive Primacy (Reversibility)
Neutralization tactics must prioritize cognitive exhaustion, tarpitting, and telemetry isolation. Destructive payloads, unauthorized lateral movement outside the defined lab/perimeter scope, or permanent host modifications are strictly prohibited and blocked at the tool-allowlist level.

### 11. Asymmetric Compute Ceiling
Defensive subagent swarms operate under a strict token and compute cap enforced by `llmpool/`. If a hostile ARTEX instance fails to stall or exhaust its inference budget within the allocated defensive ceiling, the swarm automatically disengages and escalates to static network isolation.

### 12. Strict Sandbox & Perimeter Binding
Loop D inherits ARTEX's immutable scope checks. Counter-subagents cannot follow hostile C2 channels or state-sync endpoints across external network boundaries; external indicators are logged to `evidence/` for human review rather than pursued autonomously.

### 13. Live Engagement Does Not Equal Harness Adoption
Consistent with Rule 1 of `RSI.md`, counter-tactics generated dynamically during a Loop D skirmish are ephemeral. Any novel deception or containment strategy discovered during live counter-emulation must be extracted as a behavioral delta, rebuilt clean-room by the **Builder**, and validated against held-out benchmarks before entering the permanent Capsule Registry.

### 14. Hash-Chained Engagement Receipts
Every state transition—from initial signature detection (`candidate`) to Governor sign-off (`approved`), subagent deployment (`active`), and termination (`contained`)—must produce an immutable, hash-chained receipt stored in `evidence/` with per-module attribution.

---

## State Machine Lifecycle

```text
[PASSIVE TELEMETRY] 
       │
       ▼ (≥ 3 Registry Signatures Matched)
[CANDIDATE IDENTIFIED] ──► (Fails Scope/Auth Check) ──► [LOG & DROP]
       │
       ▼ (Passes JEV Governor Gate + Owner Flag Active)
[SWARM DEPLOYED] (Illusionist / Tarpit / Sanitizer / Disruptor)
       │
       ├─► (Hostile Inference Exhausted / Looped) ──► [CONTAINED]
       ├─► (Compute Ceiling Reached) ───────────────► [DISENGAGE & ISOLATE]
       │
       ▼
[POST-MORTEM EXTRACTION] ──► Novel Deltas routed to Loop C (Scout -> Builder)
```

---

## Safety & Governance Notice

Like the core REVENANT overlay, **Loop D ships disabled (`ENABLE_LOOP_D=false`)**. Enabling active counter-emulation requires explicit owner configuration per runtime session and is intended exclusively for controlled adversary-emulation labs and authorized defensive perimeters.
