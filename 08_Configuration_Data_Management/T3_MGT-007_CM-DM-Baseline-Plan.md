# Configuration and data management baseline plan

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| MGT-007 | v0.1 | Draft | Jash Joshi | 2026-10-29 |

## 1. Purpose

Keep every project item identified, versioned and controlled, so the team always works on the right version and baselines can be reproduced.

## 2. Roles

- **Configuration manager:** Jash Joshi (proposed). Keeps the register, assigns CI numbers, checks pull requests, runs baselines.
- **Backup for model and requirements:** Vladislav Zagorodnyuk.
- **CI owners:** update their items and versions.

## 3. Configuration identification

- Every item is a configuration item (CI) with an ID `<CAT>-<NNN>`, listed in the [configuration register](T3_MGT-001_Configuration-Register.xlsx).
- File names, versions and categories: [CONTRIBUTING.md](../CONTRIBUTING.md).

## 4. Baselines

| Baseline | Review | Content | Tag |
| --- | --- | --- | --- |
| Functional | SRR | Mission and NGO, stakeholders, system requirements, ConOps | `srr-baseline` |
| Allocated | PDR | Technical requirements, MBSE model (OA, SA, LA), interfaces, plans: all 9 PDR deliverables at v1.0 | `pdr-v1.0` |
| Product | CDR | Detailed design (later phase) | `cdr-v2.0` |

## 5. Change control

Before a baseline: pull request with one approval. After a baseline: change request issue → impact assessment → approval by at least 3 of 4 members → pull request → version +0.1 → register Change log.

## 6. Status accounting and audits

- The register shows version and status of every CI; the README shows PDR deliverable status.
- Before each baseline, the configuration manager checks that every listed CI exists in the repository with the right name and version.

## 7. Data management

| Topic | Rule |
| --- | --- |
| Storage | GitHub repository `VladZg/NESR` is the master copy |
| Formats | Source files (Capella zip, xlsx, md) plus exports (png, svg, pdf) |
| Large files | Keep single files under 50 MB; Capella project zipped |
| Backup | GitHub releases at each baseline; local clones of all members |
| Access | Team members are collaborators; `main` protected |
| Retention | Nothing is deleted; superseded files stay in git history |

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.1 | 2026-10-29 | Jash Joshi | First version in the repository |
