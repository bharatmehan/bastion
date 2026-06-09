# Security Policy

Bastion is in early alpha and not yet production-ready. Security reports are still welcome because the project is being designed around authentication, authorization, delegation, and auditability.

## Reporting a Vulnerability

Please do not create a public GitHub issue for suspected vulnerabilities.

Report privately using [GitHub Security Advisories](https://docs.github.com/en/code-security/concepts/vulnerability-reporting-and-management/repository-security-advisories) for this repository when available. If advisories are not enabled yet, contact the maintainer privately through the email or contact method listed on the GitHub profile.

Include as much detail as you can safely share:

- affected commit or version
- reproduction steps
- expected impact
- whether secrets, tokens, credentials, or user data may be exposed
- suggested fix, if known.

## Scope

Security-sensitive areas include:

- authentication and token issuance
- OAuth/OIDC flows
- PKCE and redirect URI validation
- token audience and issuer validation
- agent registration and lifecycle management
- delegated scope calculation
- session, refresh token, and revocation behavior
- audit log integrity
- webhook signing
- rate limiting
- configuration loading
- secret handling
- protected-resource and MCP authorization examples

## Current Support Status

No production versions are supported yet.

| Version | Supported |
| --- | --- |
| pre-0.1 | No |

## Security Design Defaults

Bastion should prefer:

- short-lived access tokens
- explicit token audience
- exact redirect URI validation
- PKCE for authorization-code flows
- least-privilege scopes
- revocable agent credentials
- audit logs that preserve user and agent provenance
- no logging of secrets or bearer tokens

## Disclosure

The project will coordinate fixes privately before public disclosure when practical. Public advisories should avoid publishing exploit details until a fix or mitigation is available.
