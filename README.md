
# ZeroTrust ControlTrace Investigator

Identity Investigation, Control Reconciliation & Compliance Intelligence**

> Do not trust the workflow status. Verify the actual state.

## 🎥 Project Demo

[▶ Watch the ZeroTrust ControlTrace Video Demo](https://www.loom.com/share/04026479ac524bb5b6b4dc2e17bf3c4d)

> This demo walks through the synthetic investigation workflow, evidence reconciliation, findings, compliance mapping, corrective actions, and case reporting.

---

ZeroTrust ControlTrace is a synthetic cybersecurity portfolio proof of concept that explores a simple assurance problem: an IAM or ITSM workflow can report success while the actual downstream access state is still wrong.

The platform compares expected identity/access state with observed state across synthetic enterprise records, opens an evidence-backed investigation when they disagree, correlates a timeline, separates confirmed findings from assumptions, maps potential compliance relevance, assigns corrective actions, and produces an investigation case report.

## Why I built it

The project grew from the intersection of my doctoral research into Zero Trust concepts and my professional IAM / access-governance background. I wanted to apply a verification mindset to a practical question:

How do we independently validate that the security state produced by an identity-lifecycle workflow is actually correct?**

This is a zero-trust-inspired assurance pattern, not a claim that the project implements a complete enterprise Zero Trust Architecture.

## Featured scenario

 ZTCT-001 — Workflow Complete, Access Persists**

- HRIS: employee terminated
- ServiceNow: deprovisioning ticket `CLOSED COMPLETE`
- SailPoint IdentityIQ: lifecycle workflow `SUCCESS`
- Active Directory: correctly disabled
- Okta: correctly suspended
- CyberArk: privileged membership still `ACTIVE`
- Legacy application: local account still `ACTIVE`
- Splunk / PAM evidence: post-termination activity recorded

Investigation question: Why does the control record say success while target-system evidence says otherwise?

## Four synthetic demo scenarios

| Case | Investigation pattern | Main lesson |
|---|---|---|
| ZTCT-001 | Workflow complete, access persists | Workflow completion is not proof of downstream control effectiveness |
| ZTCT-002 | Orphaned privileged service account | Non-human identities need current ownership, dependency validation, and privilege review |
| ZTCT-003 | Certification approved, role does not support access | Approval evidence is not proof that an entitlement is appropriate |
| ZTCT-004 | Identity anomaly after role transfer | Residual mover access plus authentication anomalies require correlation, not premature attribution |

## Workflow

```text
HR / ServiceNow / SailPoint
          |
          v
   Expected access state
          |
          +------------------------------+
          |                              |
          v                              v
   Control reconciliation      Downstream evidence
                               AD / Okta / CyberArk /
                               Legacy Apps / SIEM
          |                              |
          +--------------+---------------+
                         v
                   Discrepancy?
                         |
                         v
        Evidence + Timeline + Findings
                         |
             +-----------+-----------+
             |                       |
             v                       v
      Compliance mapping      Corrective actions
       (advisory only)       owner / due / closure
             |                       |
             +-----------+-----------+
                         v
                 Case report / JSON
```

## Architecture

The project deliberately uses a hybrid design.

### Deterministic components
- expected-state comparison
- mismatch detection
- SHA-256 evidence digest generation
- structured case fields
- action ownership and closure fields

### AI-assisted / reasoning-support components
- evidence synthesis
- investigation-question support
- root-cause hypotheses
- executive narrative
- potential control-relevance mapping

### Human-owned decisions
- identity attribution
- malicious intent
- regulatory applicability
- NERC CIP applicability
- final compliance determination
- final finding approval
- case closure

## Investigation agents

1. Evidence Integrity Agent — provenance and reproducibility
2. Control Reconciliation Agent — expected vs observed state
3. Investigation Agent** — timeline, findings, observations, evidence gaps
4. Root Cause Hypothesis Agent — testable investigative leads
5. Compliance Mapping Agent — advisory control relevance
6. Corrective Action Agent — owner, due date, status, closure evidence
7. Executive Narrative Agent — management-ready synthesis from validated facts
8. Investigation Quality Agent — provenance, human-review guardrails, ownership, closure checks

## Framework coverage

The proof of concept uses selected areas from:

- **NIST CSF 2.0** — identity/access control, monitoring, incident analysis and investigation
- **NERC CIP** — selected access-revocation and incident-response areas for qualified review in applicable environments
- **SOX / ITGC concepts** — logical access, joiner-mover-leaver controls, privileged access and evidence of control operation
- **ISO/IEC 27001 concepts** — identity lifecycle, access rights and privileged access governance

Framework output is **advisory only**. The software does not certify compliance, determine legal applicability, or declare a violation.

## Evidence discipline

Each synthetic evidence record includes:
- evidence ID
- source
- record type
- event timestamp
- structured details
- SHA-256 digest

The hash demonstrates provenance thinking; it is **not presented as a complete legal chain-of-custody system**.

## Run locally on macOS

1. Download or clone the repository.
2. Open the project folder.
3. Double-click `START_HERE.command`.
4. The local browser dashboard opens automatically.

The interview build uses only local synthetic data and is designed to run without live enterprise connectors.

## Privacy and ethics

- Synthetic records only
- No employer, recruiter, or client data
- No production credentials
- No automatic disciplinary or regulatory decisions
- Human review required for attribution, intent, applicability, findings, and closure

## Repository guide

```text
ZeroTrust_ControlTrace/
├── START_HERE.command
├── app.py
├── cases/                  # Four synthetic investigation scenarios
├── agents/                 # Investigation and control-support modules
├── engine/                 # Orchestration
├── frameworks/             # Advisory control catalog
├── static/                 # Local dashboard
├── outputs/                # Sample investigation reports
├── docs/                   # Architecture, demo and interview documentation
└── tests_smoke.py          # Basic scenario validation
```

## What I would build next

- approved read-only connectors for identity, PAM, ITSM and SIEM platforms
- analyst approval workflow and case collaboration
- configurable organization-specific control libraries
- role-based access control for investigators
- immutable audit logging and evidence storage
- secrets management and connector authorization
- labeled test cases with measured false-positive / false-negative behavior
- workflow metrics for investigation aging and corrective-action closure

## Important boundary

This repository is a portfolio proof of concept. It is not a production compliance platform and does not replace IAM, SIEM, ITSM, incident response, legal, audit, or compliance professionals.
