# Roadmap

This roadmap is intentionally narrow. Bastion should earn trust by doing one important thing well before expanding into a general identity and authentication platform.

## Current Status

Bastion is early alpha. The project is in public foundation-building mode:

- clarify product positioning
- document the security model
- define the first runnable demo
- then implement the smallest useful core

## v0.1.0-alpha: Agent Delegation Demo

Goal: demonstrate the Bastion wedge end to end.

- Agent registry with lifecycle states: active, suspended, revoked.
- Admin-defined agent scope ceiling.
- User-approved delegated scopes.
- Effective-scope calculation: requested scopes intersected with agent ceiling and user consent.
- OAuth-style authorization-code flow with PKCE for agent delegation.
- Short-lived access token with user, agent, audience, and scope context.
- Protected-resource example that validates audience and scopes.
- Audit events for agent creation, delegation approval, token issuance, resource access, suspension, and revocation.
- Local quickstart that runs in minutes.

## v0.2.0-alpha: Developer Experience

Goal: make Bastion understandable and useful to early adopters.

- Clean CLI or server entry point.
- Docker Compose quickstart.
- Example app using a protected API.
- Example MCP server authorization flow.
- Minimal TypeScript example client.
- Expanded docs for token claims, scopes, and revocation behavior.
- Integration tests for delegation and revocation paths.

## v0.3.0-alpha: Security Hardening

Goal: make the model reviewable by security-minded developers.

- Threat model updates based on implementation.
- Token audience and issuer validation examples.
- Refresh-token and session revocation semantics.
- Rate limiting on public auth endpoints.
- Structured audit export format.
- Security checklist for self-hosted deployments.
- Fuzz or property tests for scope parsing and policy decisions where practical.

## Later

These are intentionally deferred until the core wedge is useful:

- Broader human authentication methods.
- Enterprise SSO.
- Organization and tenant management.
- Admin UI.
- SDKs for more languages.
- Hosted Cloud.
- Policy engine integrations.
- Compliance reporting.

## Non-Goals For Now

- Competing with mature general-purpose identity providers feature-for-feature.
- Adding many login methods before the agent delegation model is excellent.
- Building a large UI before the protocol and audit model are clear.
- Claiming production readiness before independent review and real deployments.
