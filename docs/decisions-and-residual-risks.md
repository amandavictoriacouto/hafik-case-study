# Decisions, Residual Risks and Release Criteria

**Milestone 03:** IN PROGRESS\
**Deployed A/B isolation and release readiness:** NOT VERIFIED

## Product and technical decisions

| Decision | Rationale and trade-off |
|---|---|
| Prioritize privacy before feature expansion | Address a P1 cache-isolation risk before adding integrations; no claim of a confirmed production incident |
| Enforce ownership in PostgreSQL RLS | Browser CRUD uses user-scoped access; child records also require owned parents |
| Apply complementary client controls | User keys, cancellation, AbortSignal, session generations and state reset protect different authentication-transition paths |
| Keep AI execution server-side | Authenticated server functions protect provider credentials; enforceable usage limits still need validation |
| Use a disposable local RLS environment | Synthetic identities and rollback reduce risk to personal data; local tests cannot establish deployed enforcement |
| Keep public environment configuration tracked temporarily | Preserve existing integration until independent provisioning is verified; private credentials must never enter tracked files |
| Support manual Markdown portability | Obsidian compatibility through manual import/export; automatic synchronization is not implemented |
| Preserve zero-additional-spend constraints | Use existing tools and free local validation; platform allowances and AI availability are dependencies, not guaranteed unlimited capacity |
| Preserve Lovable/GitHub history | Use forward changes and review; do not rewrite published history |

## Residual risks

| Priority | Risk or gap | Next evidence required |
|---|---|---|
| High validation priority | Real A/B database enforcement is NOT VERIFIED | Bidirectional synthetic CRUD, forged ownership, known IDs, child relationships and anonymous API tests |
| High validation priority | Deployed cache/session races are NOT VERIFIED | Account switching, cross-tab logout, pending requests and delayed mutations/exports |
| High validation priority | Absence of privileged credential exposure in deployed browser artifacts is NOT VERIFIED | Sanitized review of delivered chunks and request/configuration paths |
| High validation priority | Runtime JWT forwarding is NOT VERIFIED | Authenticated negative-path behavior and existing safe runtime observability where available |
| Medium validation priority | sandbox_exec isolation relies on a platform explanation | Independent technical documentation or bounded platform evidence |
| Medium validation priority | Source-to-deployment revision mapping is incomplete | Distinct local/GitHub/Lovable revision records and deployment evidence |
| Medium validation priority | Lovable environment provisioning remains unverified | Confirmed build/server provisioning before reconsidering tracked public configuration |
| Product reliability priority | AI spending boundaries, chat failures and Markdown/export edge cases remain open | Focused validation without unapproved paid calls |
| Evidence quality priority | Raw local/Preview execution artifacts are not attached | Sanitized originals or explicit retention of reported-result status |

These are prioritization categories, not new confirmed vulnerabilities. Source review found no confirmed active application RLS bypass or privileged credential exposure within the reviewed scope.

## Release criteria

Before declaring security validation complete:

1. Pin the tested deployment and record its relationship to the application revision.
2. Pass own CRUD and bidirectional cross-user isolation on all five tables using synthetic accounts.
3. Reject forged ownership, ownership transfer and cross-user parents; validate anonymous API denial.
4. Validate actual cache transitions, external logout and late asynchronous results.
5. Validate server authentication boundaries and document the limit of JWT-forwarding observability.
6. Inspect browser-delivered material for privileged credentials.
7. Confirm synthetic cleanup without affecting unrelated records.
8. Attach sanitized evidence or explicitly identify reported outcomes and missing artifacts.
9. Resolve relevant blockers; record accepted residual platform uncertainty with rationale and scope.

Broader MVP release readiness also requires bounded AI cost behavior, failure handling and data-portability checks. No paid AI call, deployment or configuration change is implied by these criteria.

## Closure position

Local phases 1–3 are complete according to the project owner's reports. Their documentation may close with explicit provenance and artifact limitations.

Lovable Cloud A/B isolation remains **NOT VERIFIED**. Milestone 03 remains **IN PROGRESS**. No security certification, comprehensive-audit completion or general production-readiness claim is made.

[Validation matrix](security-validation-matrix.md) · [Evidence register](evidence/README.md)
