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
- Every active repository except `tickadoo/frontend` and
  `tickadoo/tickadoo-app` uses Francis as the accountable merge authority.
  For a Francis-authored standard-risk pull
  request, this policy grants standing merge authority to the repository's
  approved automated merge steward after exact-head opposite-vendor review,
  green required CI, resolved threads, and complete reporting. The steward must
  execute trusted default-branch code, verify immutable evidence, and supply
  neither the review nor the authority it checks. Its identity and entrypoint
  must be documented in the repository instructions. A pull request authored
  by anyone else, or any protected-risk pull request, still requires Francis's
  explicit exact-head approval.
- Francis's exact-head authority may be recorded as a GitHub approval or as an
  authenticated, SHA-bound command issued by Francis from his own interactive
  session and retained in its auditable task or pull-request record. This is an
  authority record, not a steward attestation, and applies when GitHub will not
  allow Francis to self-approve his own pull request. Only
  `@francistickadoo` may use a repository protection bypass, and only after the
  steward has verified the applicable review, CI, thread, risk, authority, and
  SHA gates. A bypass never authorizes ignoring a material failing safety
  check.
- `tickadoo/frontend` is the temporary risk-based exception. Dominik has
  standing merge authority for routine frontend work only after exact-head
  opposite-vendor review, required CI, resolved threads, and complete reporting.
  Francis approval remains mandatory for protected-risk, cross-repository,
  shared-contract, and monorepo-migration work. Local frontend instructions
  define the full boundary.
- `tickadoo/tickadoo-app` has a separate app-only delegation from Francis.
  Dominik owns implementation, PR merges, Simulator/device validation and
  TestFlight delivery without per-PR Francis approval. This includes app-side
  booking display, offline ticket storage and other sensitive client code,
  but every PR requires exact-head independent opposite-vendor AI review,
  passing relevant tests and required CI, resolved material findings, and an
  auditable review record. An AI review must not be replaced by a human-only
  approval, and an author cannot supply their own independent review.
  Preserve the eligible non-author GitHub approval gate; Francis's AI may
  submit that review on his behalf from an eligible non-author GitHub account
  without asking him again for an in-scope app change. Record the submitting
  account, actual reviewer vendor and exact reviewed SHA; a delegated identity
  does not make an author's self-review independent. This delegation does not
  grant protection bypass rights.
  Howard/backend changes, shared API contracts, production data or money
  actions, new permissions/credentials, security-boundary changes, governance
  controls and monorepo migration remain outside this delegation. Public
  App Store submission/release and marketing claims stay with the designated
  release/product owner, currently Mark; app autonomy does not waive release
  acceptance tests or independently authorize a public release.

## Delivery workflow

- Work on a feature branch. Never push directly to a protected default branch.
- Open a focused pull request with customer impact, security/data impact,
  validation, dependencies, rollout, and rollback notes.
- Classify the change before merge:
  - **Protected-risk:** authentication or authorization; secrets; payments or
    financial calculations; customer or personal data; database migrations or
    backfills; production infrastructure, access, or deployment controls;
    security boundaries; destructive operations; and governance trust roots
    such as CODEOWNERS, agent authority instructions, branch-protection
    automation, or the independent reviewer and merge steward. These require
    Francis's explicit exact-head approval, except only client changes that
    satisfy every boundary of the mobile delegation above. All its listed
    exclusions retain Francis's approval requirement even in the app repo.
    Every change still requires all required CI and exact-head
    opposite-vendor review. A reviewer must execute from trusted default-branch
    code, so it may review an untrusted proposed change to its future version
    without becoming self-modifying.
  - **Standard-risk:** documentation, copy, tests, styling, isolated low-impact
    fixes, and similarly reversible work. A Francis-authored pull request may
    merge under the standing steward authority above once technical readiness
    is established. Other authors still require Francis's exact-head approval.
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
  rule above or from Francis's explicit exact-head approval.

## Brand and content

- Always write the company name as `tickadoo`, including at the start of a
  sentence. Never capitalize it.
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
