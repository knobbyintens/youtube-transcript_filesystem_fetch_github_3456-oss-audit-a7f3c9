# Third-Party Open-Source License Policy (v3.2)

This policy governs how third-party software components may be used in any
product or internal system. It applies to every component listed in
`inventory/dependencies.csv`.

## 1. License tiers

**Approved (no conditions)**
MIT, BSD-2-Clause, BSD-3-Clause, Apache-2.0, ISC, MPL-2.0, PSF-2.0,
EPL-2.0, Unlicense

**Conditional (legal review required)**
GPL-2.0, GPL-3.0, LGPL-2.1, LGPL-3.0 and any proprietary or custom license.

**Prohibited (must not be used)**
AGPL-3.0, SSPL-1.0, BUSL-1.1 and any license carrying non-compete or
field-of-use restrictions.

## 2. Verdict matrix

`distribution_type` is one of `internal-tool`, `saas` or `on-prem-binary`.

| License tier | internal-tool | saas | on-prem-binary |
|--------------|---------------|------|----------------|
| Approved     | OK            | OK   | OK             |
| GPL          | REVIEW        | BLOCK| BLOCK          |
| LGPL         | REVIEW        | REVIEW | BLOCK        |
| Custom       | REVIEW        | REVIEW | REVIEW       |
| Prohibited   | BLOCK         | BLOCK| BLOCK          |

## 3. Legal approvals

`inventory/approvals.json` records exceptions granted by the OSPO.

- An approval is **valid** when `status` is `approved` and `expires_on` is on or
  after the audit date.
- A valid approval changes a Conditional verdict (GPL, LGPL, Custom) from
  `REVIEW` to `OK`.
- Expired or pending approvals have no effect.
- Approvals **never** override a Prohibited verdict.

## 4. License evidence

`declared_license` is the value recorded by the owning team. For every component
whose `verification_required` flag is `true`, the published license text at
`license_reference_url` is authoritative and overrides the declared value.
Follow the evidence (e.g. a file that is actually AGPL rather than GPL, or
SSPL rather than a generic "custom" license). For components not flagged for
verification, the declared SPDX identifier may be accepted as-is.

## 5. Required actions

- `OK` - no issue required; record the component as approved in the audit output.
- `REVIEW` - open a tracking issue titled
  `[LICENSE-REVIEW] <component_name> <version>` asking for OSPO legal review.
- `BLOCK` - open a blocking issue titled
  `[LICENSE-BLOCKER] <component_name> <version>` describing the remediation
  (replace, isolate or obtain a compliant alternative before release).
