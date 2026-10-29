# Contributing: naming, versioning and reviews

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| MGT-008 | v0.1 | Draft | Jash Joshi | 2026-10-29 |

These rules apply to every file in the repository. The configuration manager checks them in every pull request.

## 1. File naming

**Pattern:** `T3_<CAT>-<NNN>_<Short-Title>.<ext>`

| Field | Rule | Example |
| --- | --- | --- |
| `T3` | Team prefix, always T3 | `T3` |
| `<CAT>` | Category code (table below) | `REQ` |
| `<NNN>` | CI number from the configuration register; never reused | `003` |
| `<Short-Title>` | English words joined by hyphens, each capitalised, max 5 words | `System-and-Technical-Requirements` |
| `<ext>` | Exports of the same CI share the name and differ only by extension | `.xlsx`, `.md` |

| Code | Category | Main folder |
| --- | --- | --- |
| MGT | Management, plans, rules | 04_Project_Management, 08_Configuration_Data_Management |
| REQ | Mission, stakeholders, requirements, compliance | 03_Requirements, 09_Maritime_Compliance |
| CON | Concept of operations | 02_ConOps |
| ARC | Functional and interface architecture | 01_MBSE_Model/functional_analysis, 07_Interface_Management |
| MOD | Capella model and its diagrams | 01_MBSE_Model |
| SIM | Analyses, simulations, trade studies | analysis |
| SAF | Risk, safety, reliability | 05_Risk_Analysis |
| VV | Verification and validation | 06_Verification_Validation |
| PS | Problem sets (homework) | problem-sets |
| REV | Review packages | reviews |
| REF | References | references |

**General rules**

1. Latin letters, digits, hyphen and underscore only; no spaces, no Cyrillic.
2. Underscore separates fields; hyphen separates words inside a field.
3. **No version, date or status in the file name** (`final`, `new`, `v2`, `2026-10-29`). Git keeps the history; the version lives in the document header and the configuration register.
4. Capella diagram exports start with the diagram type: `T3_MOD-007_SAB-System-Architecture.png`.
5. Exceptions: `README.md`, `CONTRIBUTING.md`, `CHANGELOG.md` and files in `.github/` keep their standard names.
6. Files sent outside the repository (course submissions) get the version added: `T3_MOD-008_System-Analysis-Diagrams_v1.0.pdf`.

**New file:** ask the configuration manager for the next CI number (or take it yourself and add the row to the register in the same pull request).

## 2. Versioning

Each CI has a version `vMAJOR.MINOR`, written in the document header and in the configuration register.

| Version | Meaning | When it changes |
| --- | --- | --- |
| v0.1, v0.2, … | Working draft | +0.1 with every merged pull request that changes the CI |
| v1.0 | Baselined at PDR | Set by the configuration manager at the PDR baseline |
| v1.1, v1.2, … | Approved change after the baseline | Only through a change request (section 4) |
| v2.0 | Next baseline (CDR) | At the next review |

**Repository baselines** are git tags plus GitHub Releases, listed in [CHANGELOG.md](CHANGELOG.md):

| Tag | Content |
| --- | --- |
| `srr-baseline` | Functional baseline: mission, stakeholders, system requirements, ConOps |
| `pdr-v1.0` | Allocated baseline: all 9 PDR deliverables at v1.0, release with the PDR package attached |

Every Markdown document starts with the CI header table and ends with a **Revision history** table (version, date, author, change). Binary files (xlsx, png, zip) keep their history in the register's Change log.

## 3. Branches, commits and reviews

1. **One issue per task.** Create it from a template in the Issues tab.
2. **One branch per issue:** `<issue-number>-<short-name>`, e.g. `12-risk-register`.
3. **Commit messages:** `[CI-ID] what changed (#issue)`, e.g. `[REQ-003] Update TR-13 after SIM-001 (#7)`.
4. **Pull request** into `main`, using the template. The PR description says which CIs changed and their new versions, and contains `Closes #<issue>`.
5. **Review:** at least one teammate approves the content; the configuration manager checks names, versions and the register. The author merges after approval.
6. `main` is protected: no direct pushes (Settings → Branches → require a pull request and 1 approval).

## 4. Changes to baselined items

After a CI reaches v1.0, it changes only through a **change request** issue (template "Change request"):

1. Author describes the change, reason and impact (requirements, interfaces, model, V&V).
2. Owners of affected CIs comment on the impact.
3. Team approves in the issue (at least 3 of 4 members).
4. Change goes in through a normal pull request; version +0.1; the register's Change log gets a row.

## 5. Tasks and the project board

- Issue types: **Task**, **PDR deliverable**, **Problem set**, **Change request**.
- Labels: `pdr:1` … `pdr:9`, `owner:<name>`, `priority:high/medium/low`, `type:*`.
- Milestone `PDR` groups everything due for the review; each problem set has its own milestone.
- Board columns: Todo → In progress → In review → Done. Moving a card to *In review* means a pull request is open.
