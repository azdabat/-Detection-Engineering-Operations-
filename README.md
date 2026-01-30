# CI/CD Pipeline for Detection Engineering (Detections-as-Code)

Detection rules are software artifacts.

To operate at scale, they must follow CI/CD discipline:

- version controlled  
- tested before deployment  
- promoted through maturity tiers  
- continuously maintained  

This repository follows a Detection-as-Code delivery pipeline.

---

## Why CI/CD Matters in Threat Detection

Without CI/CD, SOC environments degrade into:

- untracked rule edits  
- alert floods after changes  
- inconsistent detection quality  
- no rollback capability  
- “tribal knowledge” engineering  

CI/CD enables:

- safe iteration  
- reproducible detection logic  
- controlled promotion  
- operational reliability  

---

## Detection Engineering Pipeline Stages

---

### Stage 0 — Research & POC

Location:

- `Attack-Ecosystems-and-POC/`

Purpose:

- park new tradecraft  
- explore telemetry  
- prototype attack ecosystems  

Output:

- experimental queries  
- not deployable  

---

### Stage 1 — Minimum Truth Validation

Requirement:

- rule must anchor on unavoidable behavioural truth

Examples:

- TaskCache registry artifact  
- Service execution primitive  
- OAuth consent grant truth  
- Named pipe deviation  

Output:

- baseline hunt validated against telemetry

---

### Stage 2 — Composite Reinforcement Build

Adds:

- convergence joins  
- reinforcement signals  
- suppression logic  
- prevalence weighting  

Goal:

- reduce enterprise noise  
- raise fidelity

---

### Stage 3 — Production Promotion

Requirements:

- SOC-safe false positive profile  
- severity scoring  
- analyst directives  
- bounded compute impact  

Rules become:

- deployable analytics  
- alert-ready detections

---

### Stage 4 — Continuous Maintenance

Includes:

- regression testing  
- threat intel refresh  
- drift monitoring  
- tuning + lifecycle ownership  

Detection becomes a managed security capability.

---

## Automated QA Gates (Future Integration)

CI/CD validation checks include:

- schema correctness  
- join safety  
- performance bounds  
- rule scoring output  
- directive completeness  

---

## Promotion Workflow (Git)

1. Feature branch rule development  
2. Peer review (PR)  
3. QA checklist enforcement  
4. Promotion gate approval  
5. Merge into production ruleset  
6. Release notes + version tagging  

---

Detection Engineering is not query writing.

It is disciplined security software delivery.
