# Security Validation Matrix

**Milestone 03:** IN PROGRESS\
**Lovable Cloud A/B isolation:** NOT VERIFIED

## Status and provenance

- **IMPLEMENTED:** present in reviewed source; not a runtime assurance.
- **PASS — reported:** successful execution reported by the project owner; raw artifact not attached.
- **PASS — recorded:** outcome retained in earlier project documentation; not rerun here.
- **NOT VERIFIED:** insufficient execution evidence for the stated environment.
- **PLANNED:** proposed work without a completed implementation or validation claim.

## Evidence matrix

| ID | Control or scenario | Environment / method | Status | Evidence boundary |
|---|---|---|---|---|
| ENV-01 | Public/private environment handling | Private source and documentation | IMPLEMENTED | Independent Lovable provisioning remains unverified |
| CACHE-01 | User keys, cancellation, session guards, draft reset | Source plus mocked regression/route tests | IMPLEMENTED; PASS — recorded | Historical suite: 25 total tests, including 20 security-focused cases |
| BUILD-01 | TypeScript and production build | Local historical checks | PASS — recorded | Not rerun; no deployment assurance |
| LOCAL-01 | Restricted synthetic roles and memberships | Local PostgreSQL phase 1 | PASS — reported | Owner execution report; no transcript attached |
| LOCAL-02 | Disposable database ownership and access | Local PostgreSQL phase 2 | PASS — reported | No Cloud equivalence claim |
| LOCAL-03 | Own CRUD and foreign reads/writes, both directions, five tables | Local PostgreSQL phase 3 | PASS — reported | Synthetic database identities; not real application accounts |
| LOCAL-04 | Forged ownership and ownership reassignment | Local PostgreSQL phase 3 | PASS — reported | Tested local migration |
| LOCAL-05 | Foreign parents, own reassociation and cascades | Local PostgreSQL phase 3 | PASS — reported | Physical cascade inspection separated from user assertions |
| LOCAL-06 | Anonymous denial | Local PostgreSQL phase 3 | PASS — reported | Privilege denial and RLS behavior exercised separately |
| LOCAL-07 | Rollback and cleanup | Local PostgreSQL phase 3 | PASS — reported | Execution report; executed harness fingerprint not attached |
| PREVIEW-01 | Anonymous redirect to /auth | Lovable Preview, manual | PASS — reported | Not API authorization evidence |
| PREVIEW-02 | Registration, email confirmation and login | Lovable Preview, manual | PASS — reported | Not cross-user isolation |
| PREVIEW-03 | Main-route visual smoke checks | Lovable Preview, manual | PASS — reported | Not full functional or database validation |
| CLOUD-01 | RLS, owner policies, foreign keys and role metadata | Earlier live metadata audit | PASS — recorded | Point-in-time configuration evidence |
| CLOUD-02 | Own CRUD through actual application accounts | Deployed application | NOT VERIFIED | Complete five-table execution evidence absent |
| CLOUD-03 | Known-ID A/B reads, updates and deletes | Deployed application | NOT VERIFIED | Repeat in both directions using synthetic fixtures |
| CLOUD-04 | Forged user_id, ownership transfer and foreign parents | Deployed application | NOT VERIFIED | Valid payloads needed to exclude unrelated failures |
| CLOUD-05 | Anonymous API denial | Deployed application | NOT VERIFIED | Redirect alone is insufficient |
| CLOUD-06 | Account changes, external logout and late requests | Deployed application | NOT VERIFIED | Mocked coverage does not prove runtime behavior |
| JWT-01 | JWT attachment, validation and forwarding | Source | IMPLEMENTED | Server-to-Supabase runtime hop NOT VERIFIED |
| SECRET-01 | No privileged credentials delivered to browser | Deployed artifacts | NOT VERIFIED | Source review found no confirmed exposure within scope |
| PLATFORM-01 | sandbox_exec operational isolation | Platform explanation | NOT VERIFIED | No independent technical substantiation |
| PORTABILITY-01 | Manual Markdown import/export | Source | IMPLEMENTED with limitations | Full reliability validation pending |
| AI-01 | Runtime quality and enforceable spending limits | AI integration | NOT VERIFIED | Server integration exists; no measured quality/cost outcome |
| RELEASE-01 | Overall release readiness | Combined gates | NOT VERIFIED | Milestone remains IN PROGRESS |

## Interpretation

Local PASS results must not be relabeled as Cloud PASS. Missing logs are an artifact gap, not evidence of failure; they limit independent reproducibility. A test plan or visible UI success cannot establish database isolation.

Future executions should record expected and actual results, affected-row counts, owner-side fixture checks, version/environment and cleanup. Network errors, malformed payloads and foreign-key failures are inconclusive for RLS denial.

[Evidence handling](evidence/README.md) · [Residual risks and release criteria](decisions-and-residual-risks.md)
