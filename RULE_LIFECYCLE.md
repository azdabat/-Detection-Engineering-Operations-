# Rule Maturity Lifecycle (POC → Production)

Threat detections are not “done” immediately.

They evolve through maturity tiers until they become operationally reliable.

This repository follows a structured lifecycle model.

---

## Tier 0 — Research / Experimental POC

Purpose:

- Park new threat tradecraft  
- Prototype attack chain logic  
- Explore telemetry feasibility  

Characteristics:

- High noise  
- Limited suppression  
- Not deployable  

Location:

- `Attack-Ecosystems-and-POC/`

---

## Tier 1 — Minimum Truth Hunt

Purpose:

- Identify the unavoidable behavioural anchor  

Examples:

- TaskCache registry write  
- Named pipe creation anomaly  
- Service installation truth  

Characteristics:

- Behaviour-first  
- Minimal enrichment  
- Validated telemetry  

---

## Tier 2 — Composite Reinforced Hunt

Purpose:

- Add convergence and reinforcement signals  

Adds:

- Join-based correlation  
- Context enrichment  
- Org prevalence weighting  
- Confidence scoring  

Characteristics:

- Reduced noise  
- Higher fidelity  
- Threat-hunter oriented  

Location:

- `Production-READY-Composite-Threat-Hunting-Rules/`

---

## Tier 3 — Production-Ready Detection

Purpose:

- Deployable detection logic for SOC operations  

Requirements:

- Noise suppression gates  
- Severity scoring  
- Analyst directives embedded  
- Stable telemetry assumptions  

Characteristics:

- Low false positive rate  
- SOC-ready output  
- Patch-resistant behavioural design  

---

## Tier 4 — Managed Detection Module

Purpose:

- Continuous lifecycle ownership  

Includes:

- Drift monitoring  
- Scheduled tuning  
- Threat intel refresh  
- Regression testing against new tradecraft  

This is the stage of a mature detection engineering function.

---

## Summary Table

| Tier | Name | Deployable? | Purpose |
|------|------|------------|---------|
| 0 | POC / Research | ❌ No | Explore new threats |
| 1 | Minimum Truth Hunt | ⚠️ Partial | Validate behavioural anchor |
| 2 | Composite Reinforced | ✅ Yes | High-fidelity hunting |
| 3 | Production Detection | ✅ Yes | SOC alert-ready |
| 4 | Managed Module | ✅ Yes | Continuous improvement |

---

Detection Engineering is not query writing.

It is an operational system with maturity, promotion, and lifecycle control.
