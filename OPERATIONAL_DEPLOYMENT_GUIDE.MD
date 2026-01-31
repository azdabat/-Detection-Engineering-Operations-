# Operational Deployment Guide — Ecosystems, Cousins, Chains, and Severity (Sentinel Model)

This section explains how to deploy the **Minimum Truth Composite Framework** in production without falling into monolithic kill-chain logic.

The core principle:

> **Not every ecosystem becomes an attack chain.**  
> Some ecosystems are *capability sensors*, not *story stages*.

This is what makes the framework operationally scalable.

---

## The Three Ecosystem Types (Complete Model)

Most SOCs incorrectly treat every detection as part of a linear intrusion story.

In reality, there are **three distinct ecosystem classes**:

| Ecosystem Type | What It Represents | Example Rules | Incident Behavior |
|--------------|-------------------|--------------|------------------|
| **Capability / Cousin Ecosystem** | Attacker footholds + technique surfaces | TaskCache persistence, Service ImagePath writes, Run keys | Often **HIGH immediately** |
| **Attack-Chain Ecosystem** | Multi-stage intrusion progression | Ingress → Execution → C2 | Escalates to **CRITICAL** when stages converge |
| **Exposure / Risk Ecosystem** | Preconditions + attack surface posture | Internet-facing CVEs, weak auth, risky OAuth grants | **No incident alone**, used for prioritization |

This triad is the complete operational model.

---

# 1. Capability Ecosystems (Cousin Families)

Capability ecosystems detect:

- **what the attacker can do**
- **what footholds they established**
- **what persistence surfaces exist**

They are not always part of a linear chain.

Examples:

- Registry TaskCache persistence  
- Service ImagePath persistence  
- Run key autoruns  
- WMI subscriptions  
- Credential dumping surfaces  

These are:

> **Attack capabilities / implants / footholds**

They do not require Ingress → Execution → C2 to be real.

They are already intrusion evidence.

---

## Why Cousins Don’t Always Translate Into Chains

Persistence is not a “stage.”

Persistence is a **state**.

Example:

- A RunKey pointing to PowerShell is already compromise.
- It might execute tomorrow.
- It might execute next week.
- It might never execute again.

But it is still real.

So chaining is optional.

---

## Correct Operational Rule

Capability ecosystems trigger cases immediately.

If TaskCache persistence fires:

- you don’t wait for C2  
- you don’t wait for execution  
- you investigate now  

Because:

> Persistence truth is sufficient intrusion evidence.

---

# 2. Attack-Chain Ecosystems (Narrative Stages)

Attack-chain ecosystems detect an intrusion unfolding over time.

Examples:

- Ingress Tool Transfer  
- Execution of staged payload  
- Beaconing / Named pipe C2  
- Lateral movement  

They answer:

> “Is an active operation progressing?”

---

## Attack Chains Escalate Severity

Example:

- Ingress rule fires  
- Scheduled task persistence fires  
- Named pipe C2 fires  

Now you have:

> Active intrusion chain → Critical incident

---

# 3. Exposure / Risk Surface Ecosystems (The Missing Third Type)

Exposure ecosystems are not attacker actions.

They are **preconditions**.

Examples:

- Internet-facing exploitable vulnerabilities  
- Weak authentication posture  
- High-risk OAuth app permissions  
- Misconfigured admin shares  

These do not chain.

They inform prioritization:

> “Where would an attacker go next?”

They are not incidents.

They are risk context.

---

# Sentinel / Engineering Deployment Model

The key deployment insight:

> Composite rules are sensors.  
> Correlation happens outside the rules.

---

## Step 1 — Deploy Sensors (Composite Rules)

All composites run scheduled.

They output normalized detection rows:

- Truth anchor  
- Reinforcement indicators  
- RiskScore  
- CousinFamily  
- EcosystemType  

These are always-on truths.

---

## Step 2 — Write to a Unified Detection Stream

All composite outputs land in one logical stream, e.g.:

- `CompositeDetections_CL` (custom Sentinel table)  
- Sentinel analytics output patterns  
- MDE Advanced Hunting export pipelines  

This becomes the detection backbone.

---

## Step 3 — Correlate at Only Two Layers

The framework correlates at exactly two layers.

---

### Layer A — Cousin Confirmation (Capability Reinforcement)

Cousin correlation increases confidence inside the same capability family.

Example:

If we observe:

- TaskCache silent persistence (Registry cousin)  
AND within 24 hours:

- schtasks.exe creation/modification activity (Process cousin)

Then:

> Persistence capability confirmed at high confidence

This is not a monolith.  
It is cousin reinforcement.

---

### Layer B — Attack-Type Story Chaining (Incident Escalation)

Attack-type correlation is where incidents are created.

Example:

If we observe within 6–24 hours:

- Ingress truth  
- Execution truth  
- Persistence truth  

Then:

> Intrusion chain likely → Create Incident

This is how Tier-1 sensors become Tier-2 incidents.

---

# Rule Output Normalization (Production Metadata)

Each rule should emit consistent metadata:

```kql
| extend EcosystemType="Capability"
| extend CousinFamily="Persistence.ScheduledTask"
| extend TruthType="TaskCacheWrite"
| extend AttackStage=""

```

Ingress rule:
Copy code
Kql
| extend EcosystemType="AttackChain"
| extend AttackStage="Ingress"
Exposure rule:
Copy code
Kql
| extend EcosystemType="Exposure"
| extend TruthType="ExploitSurface"
This makes Sentinel correlation effortless.
Severity Model (Simple + Correct)
Capability Truths = High by Default
Persistence surfaces are already serious:
TaskCache
Service ImagePath
Autoruns
→ HIGH
Attack Chains = Critical When Multiple Stages Confirm
Ingress + Persistence + Execution + C2
→ CRITICAL
Exposure Truths = Inform Priority Only
Internet-facing CVEs
→ No alert, but enrich cases
HunterDirectives (Operationalised Correctly)
HunterDirectives are not “extra text.”
They are embedded runbooks.
This framework enforces three directive layers:
1) HunterDirectiveSummary (Alert-Safe)
Short, immediate meaning:
why this fired
what matters
first pivot
Keep it short.
2) HunterDirectivePack (Case Enrichment)
Full SOC guidance as:
Copy code
Kql
| extend HunterDirective = pack_array(
  "Pivot into related cousin rules",
  "Scope for file drops in Temp/Public",
  "Validate signer + prevalence",
  "Escalate if unapproved persistence"
)
3) Cousin Routing Hints (Machine-Usable)
Each rule provides recommended cousin pivots:
Copy code
Kql
| extend NextBestCousins = dynamic([
  "Persistence.ScheduledTask.SchtasksClassifier",
  "Persistence.ScheduledTask.TaskCache"
])
This enables automation and consistent analyst routing.
Golden Operational Model (Minimum Truth in Production)
This framework is deployable because:
Truth defines the sensor
Reinforcement increases confidence
Cousins provide surface parity
Attack ecosystems create incidents
Exposure ecosystems provide risk context
Correlation happens outside rules
HunterDirectives become embedded playbooks
Core Deployment Rule
Composite rules detect truths.
Cousins confirm capabilities.
Attack ecosystems build incidents.
Exposure ecosystems prioritise risk.
Telemetry ecosystems keep it scalable.
This is Minimum Truth detection engineering in production form.
Copy code
