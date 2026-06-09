# Contributing to Bastion

Thanks for considering a contribution. Bastion is an early-stage security-sensitive project, so small, clear, well-tested changes matter more than speed.

## Project Direction

Bastion is focused on identity and delegated authority for AI-native applications.

The first useful version should answer:

```text
Can a human safely delegate limited, auditable access to an AI agent?
```

Please avoid broad rewrites, speculative abstractions, or unrelated platform features unless they directly support that goal.

## Good Early Contributions

- Improve README clarity.
- Review the threat model.
- Add diagrams or examples that explain agent delegation.
- Propose token claims and audit event shapes.
- Write tests for scope intersection, revocation, and confused-deputy cases.
- Build small protected-resource examples.
- Improve security documentation.

## Before Opening a Pull Request

1. Open an issue for larger changes.
2. Keep the change focused.
3. Include tests for behavior changes.
4. Update docs when behavior, configuration, or public APIs change.
5. Avoid adding dependencies unless clearly justified.
6. Do not include secrets, tokens, private keys, real user data, or production logs.

## Development Expectations

Implementation details will evolve, but the project expects:

- boring, explicit code;
- clear error handling;
- security-sensitive defaults;
- least-privilege authorization;
- deterministic tests where possible;
- no silent weakening of security checks.

## Commit Messages

Use concise, descriptive commits:

```text
docs: add initial threat model
auth: validate token audience in resource example
agents: reject scopes above agent ceiling
```

## Security Issues

Do not report vulnerabilities in public issues. Follow [SECURITY.md](SECURITY.md).
