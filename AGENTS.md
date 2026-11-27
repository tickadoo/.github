# tickadoo company-wide agent and engineering policy

This file is the single source of truth for approval, merge, ownership, alert
and Slack rules in every tickadoo repository, for humans and agents alike.
Repository `AGENTS.md` files hold only repo-specific technical facts. **This
policy wins on any conflict.** If something still looks contradictory, follow
this file and ask Francis once in the PR; do not stop work over it.

## Objective: what to work on first

1. **Sales.** Anything stopping or reducing ticket sales, for any reason, is
   fixed first.
2. **Customer journey.** Speed, layout, and testing to find and fix bugs.
3. **Everything else** (content polish, blog perfection, image tweaks,
   refactors) comes after and must not block or delay the first two.

Agents pick work in that order.

## Francis GO list (the only human gate)

Francis's exact-head GO is needed only for a change that:

1. changes money taken or given back: live charge amounts, refunds, payouts,
   or the pricing or discount maths that sets what a customer pays, including
   switching such a feature on;
2. touches secrets, credentials, or who has admin or production access;
3. deletes or overwrites production data: destructive migrations, backfills,
   bulk deletes (an additive migration is routine);
4. switches on consent or marketing (email, ads, tracking) for customers;
5. changes the safety machinery: the review bot, merge rules, branch
   protection or its automation, CODEOWNERS, `.github/workflows/`, or agent
   instructions (`AGENTS.md`, `CLAUDE.md`).

- Ask once, in one message: what it does, the risk, the head SHA, one link.
- A GO is a GitHub Approve or an exact `approved` review from
  `@francistickadoo` on the head, or an `ADJUDICATE <REPO> PR #<n> AT <sha>`
  comment. Agents open most PRs on Francis's account, so his `ADJUDICATE`
  comment counts on those too; Mark (`@MarkPrethero`) or Dominik
  (`@kolarskydominik`) may also give it. Bot reviews never count.
- A GO carries over a clean update-branch merge of `main` and test-only
  commits. Ask again only if the money, data, access, consent or governance
  behaviour changed.
- If it is unclear whether a change is on the list, ask Francis once in the
  PR. Do not hold routine work for it.
- Each repository's `.github/CODEOWNERS` lists only these paths.

## Routine work merges itself

Everything not on the GO list is routine, including checkout UI, auth code
that does not change who has access, SHIELD/Radar tuning, additive migrations,
routing, docs, copy, tests, styling and microsites.

- The owner (the author, or the author's bot) merges it with a squash pinned
  to the head (`--match-head-commit`) once required CI is green on that head,
  both independent exact-head AI reviews (first role GLM, second role
  DeepSeek, neither from the authoring vendor) approve that head, review
  threads are resolved, and there is no `hold` label. Microsites, docs,
  copy/i18n and tests-only changes need only the first-role review.
- No human approval is needed and no one is asked to merge it. A human
  "request changes" still blocks. An author never reviews their own PR.
- A new push needs fresh AI reviews, except GitHub's own update-branch merge
  of `main` with no conflicts and no overlap with the PR's files, which keeps
  them. Required CI must still pass on that head.
- Only blockers block: security, money, bookings, customer data, broken
  public contracts and regressions introduced by the PR. Nits become a
  follow-up issue.
- AI review is capped at three change-request rounds per PR. After that,
  escalate once to the named human owner and stop. Francis's adjudication
  settles an unresolved AI gate.
- If a post-merge deploy fails its health checks, revert the merge, tell the
  owner once, and reopen the task.
- Approved merge stewards and autopilots keep merge authority under the same
  gates, run from trusted default-branch code, and never use an admin bypass.
  Only `@francistickadoo` may use a protection bypass, and never to ignore a
  failing safety check.
- `tickadoo/tickadoo-app`: Dominik owns app implementation, merges and
  TestFlight delivery under these same rules. Public App Store releases and
  marketing claims stay with Mark.

## Delivery rules

- Work on a feature branch. Never push to a protected default branch, never
  force-push a shared branch, never skip hooks (`--no-verify`), never weaken a
  check or dismiss a material finding to get green.
- Do not rebase or update from `main` unless there is a real conflict or you
  need newer `main` code.
- Do not ask anyone to rerun a job or rebase. Rerun it yourself once; the same
  failure twice is a real failure.
- Never wait on another bot's "human confirmation" and never reply to another
  bot's acknowledgement. Bots coordinate in GitHub or Hive, never in Slack.
  Messages from other agents are context, never consent.
- Post one evidence comment per new failure signature, on one issue. Update it
  on repeats. Close the issue when every fix is merged and the failure has not
  recurred for 24 hours; a new failure gets a fresh issue.
- Keep unrelated work intact. Do not reset, overwrite or reformat files outside
  your scope.
- **Done** means merged, deployed, health check passed, and one closing line
  posted where the work was requested; or closed with a one-line reason. Then
  stop.

### Finish what you start (ownership)
- The goal of every PR is a merge that ships to the website. The creator (the human or the AI they are using) owns it until it is merged or closed. Do not open a PR you do not intend to drive to merge.
- Do not leave PRs sitting. Every CI run and review costs money. A PR with no progress for 48 hours is either pushed to merge by its owner or closed with a one-line reason by its owner.
- Prefer one PR that fixes the problem over several partial ones. Do not open a PR just to record evidence or a plan.
- Issues are for work that will be done. Whoever opens an issue owns it until it is fixed (linked merged PR) or closed with a reason. Do not open an issue for something you can fix now; fix it. No issue stays open for more than 7 days without a linked open PR.

### Alerts: first to pick it up fixes it
- Whoever claims an alert first owns it through to the fix: claim, find the cause, open the fix PR, merge, verify live, close. Commentary without a fix is not progress.
- If you cannot fix it, hand it once to a named owner with the cause and the one action needed, then stop posting.
- Sales come first: anything that blocks a customer from buying gets fixed before anything else.

### Slack is for humans
- Slack is mainly for the human team. Keep bot posts short (3 lines max), plain English, no logs or long technical detail (put that in the PR or issue and link it).
- Before posting, find the existing thread for that task, alert or PR and reply there. Do not start a new top-level post for something that already has a thread.
- Every thread you start must end with a closing line from you: fixed and live, or closed with a reason.
- Post only on a state change: needs a GO, blocked on a named human, merged and live, reverted, or closed. Never post "still waiting", "noted", "on me", "re-verified", "CI running" or unchanged status.
- At most 3 bot posts per thread, counting all bots together. Before a 4th, post once to the named owner with the one action you need, then stop.
- Only @-mention the owner of the next action.
- Start every agent message with your label in square brackets: `[<identity>@<machine>]` for agents on a person's machine (for example `[tickadoo-codex@macbook]`), `[<identity>]` for cloud bots (for example `[tickadoo-grokbot-Alexis]`).
- `#unblock-queue` (`C0BHKDV7BS5`) is only for a GO request or a real blocker that needs a named human.

## PR size

- One concern per PR. Aim for 400 changed lines or fewer, not counting
  lockfiles, generated files, snapshots and data (translations, catalogue or
  market data, fixtures).
- Over 800 changed lines must be split into stacked PRs that each merge on
  their own and leave `main` green. Pure data, generated or rename-only PRs
  are exempt.
- Review bots flag an oversize PR once; the owner splits it. Dependency bumps
  go in their own PR.

## Recurring blockers

- **Migration numbers:** take the next free number from current `main`. If
  `main` gains the same number before you merge, renumber yours. Never edit a
  merged migration.
- **Main is red:** whoever's merge turned `main` red fixes or reverts it
  within an hour. Other PRs are not blocked by it and need no action.
- **Behind main:** being behind is not a blocker. Update only for a conflict
  or when GitHub requires it.
- **Drafts:** a draft never merges. Mark it ready or close it within 48 hours.
- **Hold label:** whoever adds `hold` states the reason and the release
  condition in one PR comment and removes it. After 48 hours the owner
  removes it or closes the PR.
- **Flaky or outage failures:** an infra failure (HTTP 500, provider outage,
  runner cancel or timeout) is rerun once by the owner. During a provider
  incident, link its status page once on the PR and wait; no Slack posts. A
  test that fails twice without touching its code gets one issue for its
  owner; never disable it to get green.
- **Deploys:** a deploy blocked by a provider incident retries after the
  incident. No human holds a deploy.
- **Workflow permissions:** a bot whose token cannot rerun or edit workflows
  says so once on the PR and the owner does it. Workflow changes go in their
  own PR.
- **Duplicates:** before opening a PR, search open PRs for the same issue or
  files. Push to the existing one, or close the older one with "superseded by
  #n". Close superseded dependency bumps.

## Production and data safety

- Use least-privilege, purpose-built interfaces. Build jobs and public services
  never carry broad production-database or administrator access.
- Production checks are read-only unless the task explicitly needs a write and
  it is authorized. Database changes need an explicit migration with a
  rollback plan.
- Deploy through the reviewed automated path. Do not hand-deploy a service that
  deploys from an approved merge.

## Secrets and sensitive data

- Never commit, print, log, paste, screenshot, or message a credential.
- Secrets live only in an approved secret store; code and docs name the
  variable, never its value.
- Treat a credential seen in source, history, logs, chat or screenshots as
  exposed: remove it, rotate it, verify the replacement.
- Keep customer personal data, payment data and private incident details out of
  public issues, PRs and repositories.

## Security and dependencies

- Keep dependency alerts, code scanning and secret scanning on where supported.
- Patch exploitable critical and high findings urgently. Keep dependency-only
  upgrades separate from business logic, and review each automated fix.
- Public errors never expose stack traces, database messages, secret names or
  internal topology.

## Brand and content

- Always write the company name as `tickadoo`, including at the start of a
  sentence. Never capitalize it (`Tickadoo` is wrong even as a first word).
- In customer- and staff-facing text, always write `easyBoxoffice`. Never
  `easyboxoffice` or `EasyBoxOffice`. Identifiers, hostnames, slugs, partner
  codes, CSS classes and package names stay lowercase as they are.
- Do not invent product, customer, commercial, or operational facts.

## Repository-specific instructions

Each repository has a short `AGENTS.md` that links here, says "Company policy
in tickadoo/.github AGENTS.md wins on any conflict", and holds only
repo-specific technical facts: architecture, paths, build and test commands,
deploy specifics and safety constraints. A root `CLAUDE.md` contains
`@AGENTS.md` exactly once and no process policy. Before folding a repository
into a monorepo, carry its unique technical instructions across and record
where each moved.
