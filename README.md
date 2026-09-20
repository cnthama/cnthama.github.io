# Self-Hosted IGA Lab: midPoint + Microsoft Entra ID

An end-to-end Identity Governance and Administration build implementing identity lifecycle management, access governance, certification, automated provisioning, privileged access, and single sign-on, across two platforms: [midPoint](https://evolveum.com/midpoint/) (open-source IGA) and Microsoft Entra ID.

Built and governed 3,000+ synthetic identities to test governance controls at a scale that mirrors a real mid-size organization, rather than a handful of demo accounts.

**Why two platforms instead of one:** midPoint gave full control over the governance model itself, building roles, certification campaigns, and SoD logic from scratch. Entra ID tested the same governance concepts against a real, unmodifiable cloud IdP's actual constraints, permission model, and workflow engine. That's the gap most self-hosted labs skip.

📄 Full case study with narrative and screenshots: see the live [portfolio page](https://cnthama.github.io/)
🐛 Real bugs hit and fixed, in Problem → Investigation → Root Cause → Resolution → Lesson format: [`troubleshooting.md`](troubleshooting.md)

---

## Skills demonstrated

**Identity Governance**
Access Reviews · Access Certification · RBAC · Segregation of Duties (SoD) · Access Remediation · Joiner/Mover/Leaver (JML) · Least Privilege

**Identity Administration**
Provisioning & Deprovisioning · SCIM · Microsoft Graph · Lifecycle Workflows

**Authentication & Access**
SAML · OIDC · Conditional Access · MFA · Privileged Identity Management (PIM)

**Platforms & Tools**
Microsoft Entra ID · midPoint · PowerShell · Docker · PostgreSQL · Oracle Cloud

---

## Evidence

The `evidence/` folder holds a curated set of real, redacted screenshots from the working lab, enough to show the work is real without dumping every screenshot taken along the way. All identifying details (real name, tenant name, tenant/client/object IDs, personal identifiers) have been redacted or replaced with placeholders; the underlying governance logic, roles, errors, and outcomes are shown exactly as they occurred.

| # | File | What it shows |
|---|------|----------------|
| 1 | `01-access-certification-review-list.png` | A real access certification review queue, containing actual instances of a segregation-of-duties conflict (Finance Analyst + Approver held by the same identity), a role/job mismatch, and access creep across multiple identities |
| 2 | `02-custom-governance-roles.png` | Custom governance roles designed and added (Finance Analyst, IT Support, Marketing Contributor) alongside midPoint's built-in roles |
| 3 | `03-leaver-workflow-post-offboarding.png` | A time-triggered Lifecycle Workflow leaver process: license removal, Teams removal, and account deletion chained after `employeeLeaveDateTime` |
| 4–6 | `04-scim-scope-error.png` → `06-scim-provisioning-success.png` | Full SCIM provisioning troubleshooting arc: scope-assignment error → schema-validation error → successful provisioning |
| 7–9 | `07-app-registration-400-error.png` → `09-app-registration-least-privilege-success.png` | Least-privilege app registration troubleshooting arc: two failed broad-permission attempts → narrow, correctly-scoped permission succeeding |

More screenshots exist from the build than are included here; this set was chosen to illustrate the work rather than document every step.

---

## Architecture

```
┌─────────────────────┐        ┌──────────────────────┐
│      midPoint        │        │   Microsoft Entra ID  │
│  (Docker + Postgres, │        │  (trial tenant, SCIM, │
│   Oracle Cloud VM)   │◄──────►│  Lifecycle Workflows, │
│                       │        │  Access Reviews, PIM) │
│ - 3,000+ identities   │        │                       │
│ - Custom roles + SoD  │        │ - Conditional Access  │
│ - Certification       │        │ - SSO (SAML/OIDC)     │
│   campaigns           │        │ - App registrations   │
└──────────┬────────────┘        └───────────┬───────────┘
           │                                  │
           └────────── Graph / SCIM ──────────┘
             provisioning & sync bridge
```

---

## Contact

[LinkedIn](https://www.linkedin.com/in/catherine-nthama/) · [Portfolio](https://cnthama.github.io/)
