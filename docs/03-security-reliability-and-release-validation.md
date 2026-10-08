# Milestone 03 — Security, Reliability & Release Validation

**Release:** HAFIK Lite v0.2\
**Status:** IN PROGRESS\
**Deployed A/B isolation:** NOT VERIFIED\
**Release readiness:** NOT VERIFIED

## Executive assessment

This iteration prioritizes privacy and reliability over new integrations. A source-level P1 risk involved cached data and late asynchronous results carrying across account transitions. It was an identified implementation risk, not a confirmed production exposure.

The resulting implementation combines user-scoped query keys, cancellation, AbortSignal propagation, session-generation guards and account-specific state reset. Recorded mocked tests support these controls. Database metadata and local RLS testing provide additional, distinct evidence.

The local RLS work can be documented as completed on the basis of the project owner's execution report. The broader milestone remains open because real cross-account enforcement in Lovable Cloud has not been demonstrated.

## Architecture and security boundaries

Browser reads and writes use the Supabase client with per-user RLS. The five user-data tables are conversations, messages, notes, learning_goals and study_sessions.

Messages reference conversations; study sessions reference learning goals. Child-record checks require both correct ownership and an owned parent. Deletion relationships include cascades.

The authenticated chat server function validates the user JWT through middleware and uses a client configured with that Bearer token. AI generation occurs server-side through the Lovable AI Gateway. Source review supports this design; direct runtime confirmation of the server-to-database hop remains pending.

A privileged administrative client exists in source, but the reviewed application paths had no confirmed active consumer. Absence of an identified consumer does not prove absence of all deployed privileged access.

## Implementation and recorded engineering checks

| Item | Recorded result | Boundary |
|---|---|---|
| Environment configuration hardening | Implemented | Public configuration retained temporarily; private credentials excluded from tracked configuration |
| Account-cache isolation | Implemented | Complements database authorization |
| Automated suite | 25 passing tests, including 20 security-focused cases | Historical record; mocked users/data; not rerun for this update |
| TypeScript and production build | Passed | Historical record; build success does not prove deployment |
| Pre-commit review and diff checks | Completed | Change hygiene, not security certification |

Private application traceability references:

- Environment hardening: `79e1045b8dc9f87b42e7c64eda75b77b898eede1`.
- Cache isolation: `97fbcadd88aa0f3398751f48531ceb43fce3eb2f`.

These references identify application changes, not commits in this public repository or proof of the currently deployed build.

## Local RLS phases 1–3

The phase numbering below refers to disposable local RLS setup and testing.

| Phase | Recorded completion | Provenance |
|---|---|---|
| 1 — Synthetic roles | Six roles created; restrictive attributes and two authenticated memberships verified | Project owner reported successful execution and verification |
| 2 — Disposable database | Local database created with controlled ownership and access | Project owner reported completion |
| 3 — Synthetic RLS behavior | Assertions passed across five tables, including final rollback and cleanup | Project owner reported successful execution |

PostgreSQL 17.11 was used locally with loopback-only access. Test identities were non-owner, non-superuser and NOBYPASSRLS. Membership restrictions prevented synthetic users from switching into the authenticated group role.

The reviewed harness covered own CRUD, bidirectional foreign-record denial, forged ownership, ownership reassignment, cross-user parents, anonymous access, parent reassociation and cascade checks. It separated expected authorization errors from unrelated failures, checked migration integrity and compared relevant metadata.

The final successful execution and cleanup are reported results. The transcript is not included in this repository, and the exact executed harness revision is not independently pinned by an attached artifact. No assertion count, execution date or duration is invented.

**What this establishes:** reported behavior of the tested local migration and compatibility setup.

**What it does not establish:** Lovable authentication behavior, deployed migration equivalence, real JWT enforcement, platform-role isolation or cross-user enforcement in Lovable Cloud.

## Lovable Preview checks

The project owner reported successful:

- Anonymous protected-route redirection to `/auth`.
- Account registration.
- Email confirmation.
- Login.
- Visual smoke checks of Dashboard, Memory, Learning, Chat listing, new conversation and Settings.

These are manual Preview results. They are not equivalent to public-production validation or cross-account authorization testing. Sanitized screenshots and execution records have not been attached.

## Deployed metadata and privileged-path review

The earlier live metadata audit recorded:

- All five application tables existed with RLS enabled and authenticated owner policies.
- Ownership columns and identifiers matched the expected schema.
- Both child foreign keys were validated.
- Broad table grants included anonymous and privileged roles.
- Anonymous and authenticated roles lacked BYPASSRLS; privileged platform/database roles had BYPASSRLS.
- The inspected public function and update triggers did not use SECURITY DEFINER.
- No public views or materialized views were found.

Broad grants require effective RLS; they do not alone establish an access vulnerability. Metadata inspection does not prove behavior under actual user JWTs.

The source review found no confirmed privileged credential exposure or active application RLS bypass within its scope. The platform described sandbox_exec as operationally managed, but its isolation was not independently substantiated. This remains a platform claim, not verified assurance.

## Open validation and closure decision

**Lovable Cloud A/B isolation: NOT VERIFIED.** Preparation of a test plan is not execution evidence.

Next validation covers authenticated own CRUD, known-ID foreign reads/writes, forged ownership, child relationships, anonymous denial, cache transitions, external logout, runtime JWT behavior and browser-delivered secrets inspection. Use synthetic accounts and disposable fixtures; avoid paid AI calls.

Local validation documentation can close with the evidence limitations above. Milestone 03 and release readiness remain open until the [release criteria](decisions-and-residual-risks.md#release-criteria) are met or explicit scoped exceptions are recorded.

See the [validation matrix](security-validation-matrix.md) and [evidence register](evidence/README.md). This case does not claim a comprehensive security certification.
