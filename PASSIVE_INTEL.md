# PASSIVE_INTEL.md — Open-Web OSINT & Telemetry Ingestion Specification

**Status:** Theoretical Architecture / Draft Contract  
**Overlay:** MACR (MUSE Adaptive Cognitive Runtime) — Scout Ingestion Pipeline  
**Parent Contract:** `RSI.md` & `LOOP_D.md` (Bridges External Threat Intelligence to Loops C & D)

---

## Overview

To prevent legal exposure, jurisdictional violations, and adversarial counter-detection, REVENANT's active counter-emulation (**Loop D**) is strictly confined to isolated private networks and authorized internal perimeters. 

**PASSIVE_INTEL** defines the safe, read-only boundary for gathering intelligence on rogue ARTEX deployments across the open web. Instead of interacting with external nodes, this module ingests public metadata, repository mutations, and threat-intelligence feeds offline, translating them into behavioral signatures for **Loop D** and clean-room technique deltas for **Loop C**.

---

## Architectural Separation (Air-Gap Boundary)

The ingestion pipeline enforces a strict one-way data diode between external OSINT sources and REVENANT's active runtime:

* **`scout-osint/` (Read-Only External Collectors):** Queries public APIs and threat feeds without initiating direct packets or active probes against unverified external hosts.
* **`enrich/` (Indicator Normalization & Attribution):** Parses raw OSINT artifacts (banners, headers, commit diffs) into standardized behavioral fingerprints mapped to known ARTEX fork lineages.
* **`archivestore/` (Capsule Registry Staging):** Stores verified signatures and behavioral deltas in append-only memory, making them available to both **Loop C's Builder** and **Loop D's JEV Governor**.
* **`egress/` (Abuse & Blocklist Exporter):** Formats external C2 endpoints or leaked API keys captured internally by Loop D into standardized threat-sharing formats (STIX/TAXII) for firewall blocklists or provider abuse reporting.

---

## Passive Ingestion Channels

| Intelligence Source | Collection Method | Extracted Artifacts | Downstream Consumer |
| :--- | :--- | :--- | :--- |
| **Code Forges (GitHub / GitLab)** | Public API polling & diff tracking (extends Phase 1 Scout) | Modified system prompts, stripped guardrail logic, new MCP tool definitions, custom HTTP user-agents | **Loop C (Builder)** for clean-room benchmark synthesis |
| **Internet-Wide Scan Repositories (Shodan / Censys)** | Passive metadata queries (zero active scanning by REVENANT) | Exposed `mcphttp/` web consoles, `norma/0.4` header variants, self-signed TLS cert patterns, hosting ASN trends | **Loop D (`scout-hunter`)** for internal signature matching |
| **Threat Intel & CERT Advisories** | RSS / STIX / TAXII feed ingestion | Known malicious C2 IP ranges, exfiltration domains, compromised LLM inference proxy endpoints | **Enterprise Perimeter / SIEM** for automated egress blocking |
| **Honeypot & Canary Telemetry** | Passive log aggregation from isolated external sensors | Initial reconnaissance sequences, payload delivery timing, LLM multi-agent burst cadences | **JEV Governor** for updating multi-signature thresholds |

---

## Operational Rules (Rules 15–18)

Extending the `RSI.md` and `LOOP_D.md` contracts, all open-web intelligence operations are bound by four non-negotiable constraints:

### 15. Zero Direct External Interaction
REVENANT components **must never** send active probe packets, exploit payloads, tarpit streams, or prompt-injection strings to IP addresses or domains outside the owner's explicitly authorized private CIDR blocks. All wide-area awareness must derive exclusively from third-party passive datasets or public source repositories.

### 16. Metadata-Only Ingestion (No Execution)
Consistent with Rule 8 (*Clean-Room Only*), artifacts retrieved from open-web repositories or threat feeds are treated strictly as untrusted data. Code is parsed statically for behavioral intent; external binaries or scripts are never executed inside the REVENANT host environment.

### 17. Automated Indicator Sanitization
Before external threat indicators (such as suspected C2 domains or leaked keys) are ingested into `enrich/` or `archivestore/`, they must pass through strict schema validation and prompt-injection filtering to prevent adversaries from poisoning REVENANT's memory via crafted public banners.

### 18. Outbound Egress & Responsible Disclosure
When internal Loop D containment captures active external C2 infrastructure or stolen cloud/LLM credentials targeting the owner's perimeter, REVENANT does not retaliate. Instead, `evidence/` packages the hash-chained proof into an automated alert for the local SOC, perimeter firewall, or upstream cloud provider abuse endpoint.

---

## Data Flow Lifecycle

```text
[OPEN WEB SOURCES] (Public Forks, Shodan/Censys APIs, STIX Feeds)
       │
       ▼ (Read-Only API Pull — Zero Active Probing)
[SCOUT-OSINT & ENRICH] ──► (Sanitization & Prompt-Injection Filter)
       │
       ├──► [CAPSULE REGISTRY] ──► Updates Loop D Detection Signatures
       │
       └──► [LOOP C BUILDER] ────► Clean-Room Reimplementation for Lab Sparring
```
