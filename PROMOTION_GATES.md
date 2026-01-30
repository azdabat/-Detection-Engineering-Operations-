# Promotion Gates (Detection Dev → Production)

Rules must not be deployed directly from experimentation.

They must pass structured promotion gates to prevent:

- alert floods  
- broken logic  
- operational SOC damage  
- inconsistent detection quality  

---

## Gate 1 — Baseline Truth Verified

Rule contains an unavoidable behavioural anchor.

Examples:

- `services.exe` spawning suspicious child  
- TaskCache artifact creation  
- OAuth consent grant truth  
- Named pipe deviation  

Truth is mandatory before scoring.

---

## Gate 2 — Reinforcement Convergence Present

At least one reinforcement signal increases confidence:

- SMB inbound + remote exec child  
- Task artifact + execution primitive  
- Pipe rarity + service creation  
- Baseline deviation + historical rarity  

Composite convergence is required.

---

## Gate 3 — Noise Profile Controlled

Rule tested against enterprise background:

- updater noise suppressed  
- SYSTEM baseline handled  
- prevalence weighting applied  
- false positives structurally gated  

Target: **SOC-safe fidelity**

---

## Gate 4 — Scoring + Severity Bands

Rule outputs prioritisation:

- RiskScore  
- Severity (MED/HIGH/CRITICAL)  
- Confidence explanation  

No binary spam alerts.

---

## Gate 5 — Analyst Directive Embedded

Every rule must tell analysts:

- what this likely represents  
- next pivots  
- containment priority  
- blast radius expansion  

SOC usability is mandatory.

---

## Gate 6 — Version Control + Change Safety

Rule is stored as Detection-as-Code:

- Git versioning  
- documented revisions  
- rollback possible  
- peer-review encouraged  

No silent UI edits.

---

## Gate 7 — Production Scale Safety

Rule must remain safe at large org scale:

- bounded correlation windows  
- summarize-first patterns  
- no unbounded regex joins  
- minimal compute impact  

---

## Final Promotion Decision

A rule is only Tier-3 Production when:

✅ Truth anchored  
✅ Reinforced  
✅ Noise suppressed  
✅ Scored  
✅ Analyst actionable  
✅ Operationally safe  
✅ Version controlled  

---

Detection Engineering is defensive architecture, not alert writing.
