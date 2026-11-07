# Scoped release authority and shared merge service

Status: proposed design, not active authority. This document does not override
AGENTS.md, approve a PR, authorize a bypass, or change repository protection.

## Outcome

Francis makes one decision for an explicitly bounded change and release plan.
Agents carry the work through repair, review, merge, deployment and verification
without asking the same question at each stage. Every final commit still needs
independent review and applicable checks. Mark and Dominik can contribute to
Howard, but cannot grant themselves release authority or change its controls.

## Authority is separate from readiness

A release authorization records:

- an immutable authorization ID and authenticated Francis decision reference;
- repository ID, PR number, approved baseline commit and intended outcome;
- allowed paths and explicitly permitted behavior changes;
- risk lane, affected services/environments and deployment plan;
- allowed operations: review, merge, deploy, verify, and any separately named
  migration or activation; absent operations are not authorized;
- rollback plan, expiry, revocation state and maximum permitted spend, if any.

An agent may prepare this record, but cannot attest that it issued the human
decision. A shared account name or bot-authored comment is not human evidence.
Never place credentials or private task transcripts in a public repository.

Permission persists only for this release, until expiry, revocation or a
material change. It is not permanent approval of a branch, repository or author.
Use a seven-day default expiry. Renewal is a new decision, not an automatic job.

## Successor commits

Readiness always binds to the exact final head and current base. Prior tests or
reviews do not silently carry forward. A base refresh that preserves the entire
PR patch can preserve permission, but requires renewed applicable checks and
independent exact-head review before merge.

For other successor commits, an independent reviewer must examine both the
complete final diff and the delta from the authorized baseline. The reviewer
records whether each change stays inside the authorization, with evidence.
The merge service enforces identity, path, risk, expiry and operation bounds;
the author's self-classification cannot satisfy the scope gate.

Ask Francis once with the concrete delta when the outcome, risk, data touched,
security boundary, external side effects, cost, rollout or rollback changes.
Unknown scope equivalence fails closed. Conflicts in security-critical or money
paths are material unless the original authorization explicitly described that
repair. A green check alone never answers the scope question.

## Shared reviewer and merge service

Use one reviewed implementation, installed only on explicitly inventoried active
repositories. Pilot on tickadoo/.github and Howard, then opt in siblings after
checking their actual required checks, deploy triggers and ownership rules.
Preserve frontend's existing limited domain-authority exception.

- Reviewer uses a different verified model vendor from every authoring vendor.
  Cursor is a tool, not a model vendor. Missing provenance remains a blocker.
- Execute immutable trusted default-branch workflow code, never the candidate's
  version of a reviewer, steward or authorization validator.
- Reviewer and merger have distinct least-privilege App identities and short-lived
  installation tokens. The author never supplies its own review credential.
- Review App can read the selected repo and submit reviews, not push code,
  change settings, merge, or issue authorization. Grant merge capability only
  to the separately reviewed service and within the approved repo allowlist.
- Verify exact head, current-base containment, required checks from trusted
  configuration, resolved material findings, independent review, valid scope
  and authority immediately before an atomic expected-head merge.
- Serialize merges per repository. If the head or base moves, release the
  attempt and revalidate. Do not spin repeated review jobs or cancel others.
- Keep one review session per candidate, maximum three substantive rounds.
  Infrastructure failures before review do not consume a substantive round.
  After three unresolved rounds, escalate the findings, not another bot loop.
- Preserve separate merged, deployed and live-verified records. An installation
  or merge does not enable dormant features, send messages or mutate data.

## Bootstrap without self-approval

The candidate policy or service cannot authorize its own installation or bypass.
Bootstrap needs independent review of the final implementation, green CI and a
Francis-approved exact-head rollout record listing each protection/App change.
Execute through the existing permitted owner path. If no automated owner path
exists, that initial installation is a one-time human action. Do not disable
required checks/reviews merely to install the mechanism intended to enforce them.

Keep existing rules until a test PR demonstrates that the new App's review is
accepted by GitHub, and that an unauthorized or failing PR cannot merge. Do not
assume a COMMENTED Copilot recommendation satisfies required approval or
CODEOWNER requirements. Record actual protection behavior per repository.

## Implementation and acceptance tests

1. Add a versioned authorization schema and pure fail-closed validator. Test
   forged issuer, wrong repo/PR, expired/revoked authority, unknown fields,
   changed scope, added migration, new activation and missing rollback.
2. Add the shared trusted workflow and installation allowlist. Test wrong actor,
   untrusted workflow ref, wrong App/reviewer vendor, absent provenance and
   author-supplied review evidence. Never use production tokens in PR tests.
3. Add race tests for changed head/base, newly failing CI, unresolved findings,
   duplicate jobs and authorization revocation. No successful stale merge.
4. Pilot non-production test PRs on .github and Howard. Prove authorized success
   and every denied case, including author self-approval and token misuse.
5. Update canonical AGENTS.md only with the reviewed implementation/entrypoints.
   Inventory sibling instruction files before changing pointers; preserve their
   unique content and record monorepo migration destinations.
6. Enable repositories individually. Keep a rollback that revokes the new App
   and restores the captured protection configuration without opening main.

Until these steps pass, existing exact-head authority rules remain in force.
