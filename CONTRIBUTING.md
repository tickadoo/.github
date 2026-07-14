# Contributing to tickadoo

Thank you for helping improve a tickadoo project.

## Before you start

- Open or reference an issue for material changes when practical.
- Read the repository's `README.md`, `AGENTS.md`, and local contribution notes.
- Never include credentials, personal data, payment data, or confidential
  operating details in code, issues, screenshots, logs, or pull requests.

## Making a change

1. Create a focused feature branch from the current default branch.
2. Keep the change small enough to review and roll back safely.
3. Add or update tests for behavior changes.
4. Run the repository's documented checks.
5. Open a pull request using the default template.

All pull requests need their required CI before merge. Protected-risk changes
(including auth, secrets, payments, customer data, migrations, production
infrastructure, security boundaries, and destructive operations) also need an
independent human approval from an appropriate reviewer. Authorized maintainers
may merge standard-risk, reversible changes after successful automated review.
Do not push directly to the default branch.

Repository-specific instructions may add stricter requirements. The company-wide
baseline is documented in [AGENTS.md](./AGENTS.md).
