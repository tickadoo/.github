## Summary

<!-- What changed and why? -->

## Customer impact

<!-- Customer journey, performance, accessibility, compatibility, or "None". -->

## Security and data impact

<!-- Auth, permissions, secrets, PII, payments, database, public exposure, or "None". -->

## Risk tier

- [ ] Standard-risk: reversible docs, copy, tests, styling, or isolated low-impact work.
- [ ] Protected-risk: auth, secrets, payments, customer data, migrations, production infrastructure, security boundaries, or destructive operations.

## Validation

<!-- Exact checks run and results. Include screenshots only when useful and safe. -->

## Rollout and rollback

<!-- Dependencies, deployment order, migrations, feature flags, monitoring, and rollback. -->

## Checklist

- [ ] The change is focused and preserves unrelated work.
- [ ] Tests cover the changed behavior, or the reason they do not is documented.
- [ ] Required local checks pass.
- [ ] No credentials, personal data, payment data, or internal-only details were added.
- [ ] Public errors and logs expose no sensitive implementation detail.
- [ ] Rollout dependencies and rollback steps are explicit.
- [ ] Required CI is green and every material review finding is addressed.
- [ ] Francis approval is requested, unless the repository's documented frontend exception applies.
- [ ] Protected-risk work has independent review in addition to Francis approval.
