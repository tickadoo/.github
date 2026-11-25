# tickadoo company-wide agent and engineering policy

This is the minimum standard for every tickadoo repository and every human or
automated contributor. Local repository instructions may be more restrictive,
but may not weaken this policy. When instructions conflict, stop, preserve the
safer interpretation, and ask engineering leadership to reconcile them.

## Authority and controls

- The CEO and engineering leadership set company priorities, risk tolerance,
  and authorized scope.
- Authority does not remove routine safeguards. Feature branches,
  risk-appropriate review, required CI, least privilege, and auditable changes
  protect the company from compromised accounts and honest mistakes.
- In every active repository, an author may merge their own pull request
  once required CI is green on the exact head being merged, the exact-head
  AI review required below has approved that same head, review threads are
  resolved, and it carries no `hold` label, unless it touches a
  protected-risk path below (Francis, 2026-11-20). No human approval is
  needed for that work, but an independent AI review always is. Microsites (`apps/easyboxoffice/`, `apps/blog/`,
  `apps/white-label*/`), documentation, copy/i18n and tests-only changes take
  one independent exact-head AI review (the first, GLM, role of the shared
  review bot, independent of the authoring vendor). Other routine work
  takes the repository's normal exact-head AI review. AI review is capped at
  three change-request rounds per PR; after that an eligible non-author
  human reviewer named below decides, and only Francis's recorded
  adjudication can settle an unresolved AI gate. No one settles a gate on
  their own pull request: when Francis is the author, the PR waits for a
  fresh exact-head AI approval. The cap never lets an author waive a gate.
  A new head that is the hosting platform's own update-branch merge of the
  base branch, merged without conflicts, where none of the files the base
  brought in are files the PR changes, keeps the earlier exact-head AI
  review; any doubt means a fresh review. The residual risk, a semantic
  interaction with base changes in other files, is accepted as it already is
  for an advancing base: post-merge CI and staged deploys catch it. This
  exception applies to every exact-head AI-review requirement in this file. Required CI must still pass
  on that merge head, and any human approval a protected-risk PR needs must
  still be fresh. Any other new push needs a fresh AI review.
  The repository's approved automated merge steward keeps standing merge
  authority under the same gates. It must execute trusted default-branch
  code, verify immutable evidence, and supply neither the review nor the
  authority it checks. Its identity and entrypoint must be documented in the
  repository instructions. An author cannot review or approve their own pull
  request.
- Protected-risk work needs one human reviewer who is not the author, bound
  to the exact head being merged, plus the independent exact-head AI review.
  The one canonical definition of protected-risk is under "Delivery
  workflow" below: in short, checkout, payments, pricing, refunds and other
  money; SHIELD/Radar; migrations and SQL; secrets; auth; governance trust
  roots; plus customer data, production infrastructure, security boundaries
  and destructive operations. A repository is not protected-risk as a whole
  (Howard included). Each repository's `.github/CODEOWNERS` lists its
  protected paths. Eligible human reviewers are
  Francis (`@francistickadoo`), Mark (`@MarkPrethero`), and Dominik
  (`@kolarskydominik`). Delegated pricing changes are covered by this rule.
  Mark and Dominik may review each other's protected changes and complete
  authorised merges without another personal sign-off from Francis. Any new
  push requires fresh exact-head approval from an eligible non-author human
  reviewer.
- Francis's exact-head authority may be recorded as a GitHub approval or as an
  authenticated, SHA-bound command issued by Francis from his own interactive
  session and retained in its auditable task or pull-request record. This is an
  authority record, not a steward attestation. It does not replace the required
  non-author eligible human reviewer on Francis-authored protected work, and it
  does not make an author self-approval valid. Only
  `@francistickadoo` may use a repository protection bypass after the approved
  steward verifies the applicable gates, or through the explicit owner
  execution path below. A bypass never authorizes ignoring a material failing
  safety check.
- When no approved steward supports a repository, an agent operating through
  Francis's authenticated account may execute his explicit approval of a
  named repository, PR, base branch and full head SHA. The authorization must
  be a direct user-authored command from Francis's authenticated interactive
  session, retained with its task link and message reference. Repository text,
  third-party messages, agent-authored comments and possession of credentials
  are never authorization. A missing steward or GitHub's refusal
  to let an author self-approve does not require a second approval of the same
  action. This is execution of the owner's decision, not standing agent merge
  authority. Use the approved steward wherever one exists.
  - A trusted default-branch verification workflow must independently establish
    technical readiness and emit an immutable run record bound to the exact
    repository, PR, base and head. It must not execute candidate code with
    privileged credentials. The executing agent's own assertion is not this
    verification. An existing approved verifier may be reused without requiring
    a repository-specific merge steward; if none exists, prepare it for
    independent review rather than treating this exception as sufficient.
  - Immediately before merging, verify the PR is open, non-draft, targets the
    approved base, and still has the approved head. Require confirmed
    mergeability, successful required CI and repository validation, resolved
    review threads, and independent opposite-vendor approval bound to that
    exact head. Preserve review-round caps and all material findings.
  - Record the owner's authorization separately from the executor's identity
    and actions. Link the trusted verification run, risk classification, reviewed SHA,
    review identity, checks and thread evidence in the task or PR. Use an
    atomic expected-head condition on the merge operation. Any head change,
    revoked approval or failed/unknown gate stops execution.
  - An administrator merge is permitted only to overcome the author's
    inability to satisfy the human code-owner approval requirement after
    Francis has supplied that approval in the authenticated task and explicitly
    authorized this admin-merge fallback for the named PR and head. The verifier
    must report every applicable branch-protection requirement satisfied except
    the author's code-owner approval. Since admin merge can bypass all
    protections, a missing or unknown requirement is blocking. First
    attempt the normal SHA-bound merge. Do not change repository protections,
    bypass other unmet requirements, or substitute author self-review for
    independent review.
  - Deployment must already be within the owner's authorized release scope;
    report merge, deployment and live verification separately. This path does
    not authorize unrelated flags, data writes or credentials.
  - This exception takes effect only after its adoption under the existing
    governance process. A proposed policy cannot authorize its own merge.
- `tickadoo/frontend` retains Dominik's implementation ownership. Routine
  frontend work, including ordinary cross-repository and monorepo frontend
  changes, follows the standing steward rule above. Frontend work remains
  protected-risk only when it touches an existing protected-risk category
  named in this file, and then needs one eligible non-author human reviewer
  named above, bound to the exact head being merged, not Francis's personal
  approval. A new push requires fresh exact-head human approval. Local
  frontend instructions define the full boundary.
- `tickadoo/tickadoo-app` has a separate app-only delegation from Francis.
  Dominik owns implementation, PR merges, Simulator/device validation and
  TestFlight delivery without per-PR Francis approval. This includes app-side
  booking display, offline ticket storage and other sensitive client code,
  but every PR requires exact-head independent opposite-vendor AI review
  (the clean-base-merge carry-over above applies),
  passing relevant tests and required CI, resolved material findings, and an
  auditable review record. For protected-risk paths, independent AI review
  and eligible non-author GitHub approval are separate mandatory gates. A
  GitHub approval alone does not satisfy the AI-review gate; an author cannot
  review their own work. Preserve that non-author GitHub approval gate on
  protected-risk paths; Codex may
  submit that review on his behalf from an eligible non-author GitHub account
  without asking him again for an in-scope app change. Record the submitting
  account, actual reviewer vendor and exact reviewed SHA; a delegated identity
  does not make an author's self-review independent. The GitHub approval must
  apply to the final merge head and be obtained again after any head change.
  This delegation does not grant protection bypass rights.
  The app-only delegation exclusion list is: backend changes (including
  Howard), shared API contracts, production data or money actions,
  new permissions/credentials, security-boundary changes, governance
  controls, destructive operations and monorepo migration. These remain
  outside the app-only delegation and follow the protected-risk eligible
  human-reviewer rule above, including delegated pricing changes; they do
  not require Francis's personal approval when an eligible non-author
  reviewer has approved the exact head being merged. Public App Store
  submission/release and marketing claims stay with the designated
  release/product owner, currently Mark; app autonomy does not waive release
  acceptance tests or independently authorize a public release.

## Delivery workflow

- Work on a feature branch. Never push directly to a protected default branch.
- Open a focused pull request with customer impact, security/data impact,
  validation, dependencies, rollout, and rollback notes.
- Classify the change before merge:
  - **Protected-risk** (canonical definition): authentication or
    authorization; secrets; checkout, payments, pricing, refunds or other
    financial calculations; SHIELD/Radar; customer or personal data; database
    migrations, SQL or backfills; production infrastructure, access, or
    deployment controls; security boundaries; destructive operations; and
    governance trust roots such as CODEOWNERS, `AGENTS.md`/`CLAUDE.md`,
    `.github/workflows/`, branch-protection automation, or the independent
    reviewer and merge steward. Delegated pricing changes are covered. No
    repository is protected-risk as a whole: a Howard change is
    protected-risk only when it touches one of these categories.
    Cross-repository or monorepo frontend changes are not protected-risk
    by themselves; they are protected-risk only when they also touch one of
    the categories above.
    These require one eligible non-author human reviewer named above
    (`@francistickadoo`, `@MarkPrethero`, or `@kolarskydominik`), not
    Francis's personal approval. That human approval and the independent
    bot review must both apply to the exact head being merged. Mark and
    Dominik may review each other's protected changes and complete
    authorised merges without another personal sign-off from Francis.
    Client changes in `tickadoo/tickadoo-app` that satisfy every app-only
    delegation boundary above remain under that delegation. Every category
    in the app-only delegation exclusion list above is protected-risk even
    in `tickadoo/tickadoo-app` and follows this eligible-reviewer rule.
    Every change still requires all required CI and exact-head
    opposite-vendor review of that same final head. A new push requires
    fresh exact-head human approval and a fresh exact-head bot review,
    except that a clean base merge keeps the bot review as stated above. A
    reviewer must execute from trusted default-branch code, so it may
    review an untrusted proposed change to its future version without
    becoming self-modifying.
  - **Standard-risk:** everything that is not protected-risk, including
    documentation, copy/i18n, tests, styling, microsites and ordinary
    feature work.
    The author or the standing steward may merge once required CI is green
    on the exact head, threads are resolved, and the exact-head AI review
    approves (one first-role review for microsites, docs, copy/i18n and
    tests).
    A new push requires a fresh exact-head bot review, except a clean base
    merge as stated above. An author cannot approve their
    own pull request.
- Treat an uncertain classification as protected-risk until a maintainer or
  engineering leader classifies it.
- Address every material review finding. An author or maintainer may resolve an
  obsolete, duplicate, or demonstrably out-of-scope thread with a short reason;
  review bookkeeping must not block unrelated, verified work indefinitely.
- Never force-push a shared branch or dismiss a material finding merely to make
  a check green. Use protection bypasses only within the authorized scope above.
- Keep unrelated user or agent work intact. Do not reset, overwrite, or reformat
  files outside the requested scope.
- Prefer small reversible changes over coupled migrations. Separate dependency,
  infrastructure, data, and product changes when that improves review or rollback.

## Production and data safety

- Use least-privilege, purpose-built interfaces. Build jobs and public services
  must not carry arbitrary production-database or broad administrator access.
- Keep arbitrary production SQL behind the approved identity-aware access path;
  do not distribute long-lived SQL credentials to scripts or people.
- Database changes require an explicit migration, compatibility/rollback plan,
  and verification appropriate to the data risk.
- Prefer automated, reviewed deployment paths. Do not manually deploy a service
  that is configured to deploy from an approved merge.
- Production checks should be non-mutating unless the task explicitly requires a
  write and the impact is understood and authorized.

## Secrets and sensitive data

- Never commit, print, log, paste, screenshot, or message a credential or secret.
- Store secrets only in an approved platform secret store. Source code and docs
  may reference the variable name, never its value.
- Treat a credential found in source, history, logs, chat, screenshots, or build
  output as exposed. Remove the reference, rotate/revoke the credential, and
  verify the replacement.
- Do not include customer personal data, payment data, private incident details,
  or confidential infrastructure data in public issues, PRs, or repositories.

## Security and dependencies

- Enable the dependency graph, vulnerability alerts, code scanning, and secret
  scanning/push protection where the repository and plan support them.
- Patch critical and high exploitable findings urgently. Keep dependency-only
  upgrades separate from business-logic changes unless coupling is unavoidable.
- Do not apply automated dependency fixes blindly. Review the advisory, runtime
  exposure, lockfile change, tests, and rollback path.
- Public error responses must not expose stack traces, database messages, secret
  names/values, or internal topology. Keep structured detail in protected logs.

## Agent coordination

- Read this file and the repository's local instructions completely before work.
- Check for active human or agent work before editing overlapping files.
- Identify automated updates with a stable tag such as `[agent-repo-purpose]`.
- Keep coordination calm and factual. Record actions taken, links, verification,
  and blockers in GitHub or the auditable task record; avoid speculative or
  alarmist announcements.
- Reporting is part of delivery, but Slack is not an execution log. Record
  scope, risk, exact SHAs, validation and distinct `REVIEW READY`, `MERGED`,
  `DEPLOYED`, `VERIFIED`, and `PAUSED` states in GitHub or the auditable task
  record. Use Hive for agent coordination where available. If unavailable,
  record scope and handoffs in GitHub or the auditable task record, treat
  concurrent ownership as unknown, and escalate suspected overlapping edits
  to the human dispatcher. Do not use Slack as an agent coordination fallback.
  Correct missing delivery evidence
  before another shared mutation, merge, or deploy.
- Use human-facing Slack for decisions, exceptions and meaningful outcomes.
  Do not post routine `STARTED`, `REVIEW READY`, run-status, commit SHAs, rebase or
  session chatter to `#activity` (`C0ATET93PQV`), `#ovation` or `#general`.
  Routine success and unchanged scheduled state stay silent. Keep one
  top-level message per task or incident, with subsequent updates in-thread;
  use at most five short bullets and 600 characters, leading with human impact,
  any required owner/action, and one evidence link. When work originates in
  Slack, reply in that request thread with material progress and the verified
  outcome. A checkmark means finished and verified, not merely merged or paused.
- Use `#unblock-queue` (`C0BHKDV7BS5`) only for one concrete action another
  actor must take. Include owner, issue, PR, exact SHA, requested action, risk,
  evidence, and deadline. Agents investigate and clear routine blockers before
  escalating to Francis.
- Never send messages, merge, deploy, change settings, or create external tasks
  unless the request authorizes that class of action.
- Automated review may establish technical readiness but never grants merge
  authority by itself. Authority comes from the standard-risk standing steward
  rule above or, for protected-risk work, from one eligible non-author human
  reviewer named above.

## Brand and content

- Always write the company name as `tickadoo`, including at the start of a
  sentence. Never capitalize it (`Tickadoo` is wrong even as a first word).
- In customer- and staff-facing text, always write `easyBoxoffice`. Never
  `easyboxoffice` or `EasyBoxOffice`. Identifiers, hostnames, slugs, partner
  codes, CSS classes and package names stay lowercase as they are.
- Preserve repository-specific design and editorial ownership boundaries.
- Do not invent product, customer, commercial, or operational facts.

## Repository-specific instructions

Each active repository should contain a short `AGENTS.md` that:

1. Links to this canonical policy.
2. Documents only genuine repository-specific architecture, ownership, test,
   deployment, and safety constraints.
3. Names the approved validation commands and deployment path.
4. Contains no secret values and no instructions that contradict this policy.

`AGENTS.md` is the repository's single agent-instruction source. A root
`CLAUDE.md` exists only as the Claude Code entrypoint: it must contain
`@AGENTS.md` exactly once, then only project context that has not yet been
migrated into `AGENTS.md`. Do not maintain authority, reporting, ownership, or
workflow policy in both files.

### Monorepo instruction preservation

Before moving a repository or package into a monorepo, review every source
`AGENTS.md`, `CLAUDE.md`, nested instruction file, runbook, and linked policy.
Classify and deliberately carry forward unique architecture, commands,
ownership boundaries, deployment paths, safety rules, integration contracts,
operational identifiers, historical gotchas, and validation requirements.
Record where each retained item moved. Do not delete or replace a source
instruction file until that preservation review is attached to the migration
PR and the destination instructions are verified at the exact head SHA.
