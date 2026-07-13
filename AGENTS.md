# tickadoo company-wide agent and engineering policy

This is the minimum standard for every tickadoo repository and every human or
automated contributor. Local repository instructions may be more restrictive,
but may not weaken this policy. When instructions conflict, stop, preserve the
safer interpretation, and ask engineering leadership to reconcile them.

## Authority and controls

- The CEO and engineering leadership set company priorities, risk tolerance,
  and authorized scope.
- Authority does not remove routine safeguards. Feature branches, human review,
  required CI, least privilege, and auditable changes protect the company from
  compromised accounts and honest mistakes.
- A genuine emergency bypass must be explicitly authorized, minimal, logged,
  followed by immediate verification, and reviewed afterwards. It is not the
  normal delivery path.

## Delivery workflow

- Work on a feature branch. Never push directly to a protected default branch.
- Open a focused pull request with customer impact, security/data impact,
  validation, dependencies, rollout, and rollback notes.
- Require at least one human approval and all required checks before merge.
- Never force-push a shared branch, dismiss a finding to make a check green, or
  bypass a protection rule without explicit emergency authorization.
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
- Keep coordination calm and factual. Report actions taken, links, verification,
  and blockers; avoid speculative or alarmist announcements.
- Never send messages, merge, deploy, change settings, or create external tasks
  unless the request authorizes that class of action.
- Human review must be genuinely human. An automated review does not satisfy the
  company approval requirement unless leadership explicitly changes this policy.

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
