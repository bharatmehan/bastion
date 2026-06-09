# Threat Model

This is the initial threat model for Bastion. It is incomplete by design and should be updated as implementation decisions become concrete.

## Assets

- User accounts and sessions.
- Agent identities and credentials.
- Delegation records.
- Access tokens and refresh tokens.
- Client secrets and signing keys.
- Scope and policy definitions.
- Audit logs.
- Protected resource metadata.

## Trust Boundaries

- Browser or app client to Bastion.
- Agent runtime to Bastion.
- Agent runtime to protected resource.
- Bastion to database.
- Bastion to external identity providers.
- Bastion to webhook receivers.
- Bastion to MCP servers or tools.

## Primary Risks

### Over-Broad Agent Authority

An agent receives more access than intended.

Mitigations:

- admin-defined agent scope ceiling
- user-approved delegated scopes
- resource audience checks
- fail-closed scope evaluation
- clear consent screens and audit events

### Confused Deputy

A resource server accepts a token intended for another resource, or an agent uses authority outside the intended context.

Mitigations:

- explicit audience binding
- resource-server validation examples
- token issuer validation
- no blind token passthrough

### Credential Leakage

Agent credentials, bearer tokens, refresh tokens, or signing keys are exposed through logs, config, local files, or compromised tools.

Mitigations:

- short-lived access tokens
- secret redaction in logs
- credential rotation
- separate refresh-token handling
- no example code that logs bearer tokens

### Malicious or Compromised Agent

An agent intentionally abuses granted authority or is hijacked.

Mitigations:

- least-privilege scopes
- short expiries
- agent suspension and revocation
- audit trail with user and agent provenance
- resource-side enforcement

### Consent Confusion

A user approves access without understanding which agent, resource, or scopes are involved.

Mitigations:

- explicit agent identity in consent
- human-readable scope descriptions
- resource/audience display
- easy delegation review and revocation

### Redirect and Authorization-Code Attacks

An attacker intercepts or injects authorization codes.

Mitigations:

- exact redirect URI validation
- PKCE with S256
- state validation
- short-lived authorization codes

### Audit Gaps

Security teams cannot determine whether a human or agent performed an action.

Mitigations:

- structured audit events
- user and agent IDs on delegated sessions
- request IDs
- token/delegation references
- immutable or tamper-evident audit storage in future versions.

## Non-Goals In The Initial Threat Model

- Formal verification.
- Complete enterprise compliance mapping.
- Full hosted-cloud operational threat model.
- Exhaustive coverage of every human login method.

## Review Checklist

- Does every delegated access path identify both user and agent?
- Can every token be tied to an issuer, audience, expiry, and scope set?
- Can an agent be suspended quickly?
- Can a user revoke a delegation?
- Can a resource server reject tokens not meant for it?
- Are secrets excluded from logs and examples?
- Are public endpoints rate limited?
