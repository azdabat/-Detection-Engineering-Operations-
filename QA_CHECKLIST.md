# Detection Engineering QA Checklist (Production Readiness)

Modern threat detections must be treated as engineered software artifacts.

This checklist ensures that any rule promoted into production is:

- syntactically valid  
- behaviourally grounded  
- noise-resistant  
- analyst-actionable  
- operationally safe  

---

## 1. Syntax + Platform Validation

Before anything else:

- ✅ Query executes successfully in MDE Advanced Hunting / Sentinel  
- ✅ No unresolved fields, broken joins, or scope errors  
- ✅ Uses tenant-realistic tables only  
- ✅ No unsupported operators for production analytics  

---

## 2. Minimum Truth Anchor Confirmed

Every rule must begin with an unavoidable behavioural truth.

Examples:

- Service execution via `services.exe`
- TaskCache registry artifact creation  
- OAuth consent grant event  
- Named pipe deviation  
- Unsigned driver load truth  

**Truth must exist before enrichment.**

---

## 3. Reinforcement Layer Present (Composite Logic)

Rules must not alert on single weak signals.

At least one reinforcement signal is required:

- inbound SMB + suspicious child execution  
- persistence artifact + execution primitive  
- pipe rarity + service creation correlation  
- baseline deviation + historical suppression  

Reinforcement strengthens truth — it does not redefine it.

---

## 4. Noise Suppression (Enterprise Reality)

Production rules must survive real environments.

Required controls:

- Safe vendor + safe path suppression  
- Updater / installer exclusions  
- Baseline account handling (`SYSTEM`, `NETWORK SERVICE`)  
- Org prevalence weighting where applicable  
- Avoid endless allowlists — suppress structurally  

---

## 5. Scoring + Severity Output

Rules must prioritise, not flood.

Include:

- RiskScore calculation  
- Severity bands (MED/HIGH/CRITICAL)  
- Confidence rationale  

Scoring is a triage multiplier, not a trigger.

---

## 6. SOC-Ready Analyst Directives

Every detection must output guidance:

- What does this likely represent?  
- What pivots should analysts run next?  
- What containment is appropriate?  
- What is the blast radius expansion path?  

Detection without analyst action is incomplete.

---

## 7. Performance + Scale Safety

Rules must remain safe at enterprise scale:

- Avoid unbounded joins  
- Avoid full-estate regex without anchors  
- Prefer summarize-first patterns  
- Limit enrichment windows tightly  

Target: **<5% false positives with minimal tuning**

---

## Final QA Decision

A rule is only production-ready when it is:

✅ Truth-anchored  
✅ Reinforced  
✅ Noise-suppressed  
✅ Scored  
✅ Actionable  
✅ Operationally safe
