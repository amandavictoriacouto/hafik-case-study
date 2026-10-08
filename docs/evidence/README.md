# Evidence Register and Publication Rules

This folder defines an evidence structure. It currently contains no raw execution logs, screenshots, tokens, fixtures or database exports.

## Current register

| Evidence | Available provenance | Artifact status |
|---|---|---|
| Environment hardening and cache implementation | Private application source and commit references | Public narrative only |
| Automated tests, TypeScript and build | Historical recorded outcomes | Raw output not attached; not rerun for documentation |
| Local phases 1–2 | Project owner completion reports | Transcript not attached |
| Local phase 3, rollback and cleanup | Project owner successful execution report; harness reviewed during preparation | Final execution transcript and executed revision fingerprint not attached |
| Basic Preview authentication and visual checks | Project owner manual reports | Sanitized captures not attached |
| Deployed database metadata | Earlier audit findings recorded in the case | Sanitized metadata artifact not attached |
| Deployed A/B behavior | Planning only | NOT VERIFIED; no passing artifact |

No new dates, test counts or results should be inferred from missing artifacts.

## Proposed artifact structure

When separately approved, add sanitized summaries under local-rls/, preview-auth/, deployed-isolation/ and engineering-checks/. These folders and artifacts are proposals, not existing evidence.

Each record should include:

- Evidence ID and scenario; expected versus observed result.
- Environment category and version/commit when known.
- Date when known; otherwise explicitly unknown.
- Method and provenance: source inspection, automated output, owner-reported manual execution or platform claim.
- PASS, FAIL, NOT VERIFIED or INCONCLUSIVE with a reason.
- Limitations, cleanup outcome and reviewer.
- A fingerprint of the executed script where appropriate, after private review.

Keep local, GitHub and deployed revisions distinct. A synchronized source branch does not prove the published build matches it.

## Publication rules

Never publish credentials, JWTs, cookies, authorization headers, connection strings, private environment values, personal email addresses, machine-specific paths or identifiable fixture values. Use actor and record aliases instead of raw identifiers.

Do not upload raw HAR files, Copy-as-cURL output, browser storage, account confirmation links, database dumps or unreviewed terminal transcripts. Screenshots must be cropped and redacted before publication.

The external local SQL harness is not automatically approved for publication. It needs separate sanitization and review. Keep original private evidence separate from its public summary.

Record missing evidence honestly rather than reconstructing screenshots or logs after the fact.

[Validation matrix](../security-validation-matrix.md) · [Milestone 03](../03-security-reliability-and-release-validation.md)
