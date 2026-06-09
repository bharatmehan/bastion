# Bastion

Open-source identity and delegation server for AI-native applications.

Bastion is purpose built for apps, agents and products where human users and AI agents both need secure, auditable access to tools, resources, APIs, data, and workflows.

The first goal is narrow by design: Help developers register/onboard agents, delegate user-approved scopes to them, issue standards-aligned tokens, and keep an audit trail that explains who did what, through which agent, and under which permission boundary.

> Current Status: early alpha in development. Warning: This project is not ready for production.

## Why Bastion Exists

Most authentication systems were designed around humans, service accounts, and static machine clients. And the AI Agents auth is bolted on.

But, AI-native software brings a different operating model:

- Agents act on behalf of users.
- Agents call tools, MCP servers, APIs, and sometimes other agents.
- A single workflow may involve a user, an app, an agent, a tool server, and a downstream service.
- Credentials can easily become over-broad, long-lived, hard to attribute or attenuate, and hard to revoke.

Bastion exists to make that boundary explicit.

The core idea of Bastion is:

```text
effective access = agent ceiling intersected with user delegation intersected with resource policy
```

That means an agent should never receive more authority than the system administrator allows, the user consents to, and the protected resource accepts.

## What Bastion Is

Bastion is intended to become a self-hosted identity and delegation server for AI-native applications.

The initial product surface will be:

- Agent registry: register agents as first-class principals with metadata, lifecycle state, and ownership.
- Delegated authorization: let users grant scoped authority to agents without sharing their own credentials.
- OAuth/OIDC alignment: use established web identity primitives wherever possible.
- MCP-aware authorization: support the authorization patterns emerging around Model Context Protocol servers and clients.
- Audit trail: record user, agent, client, scope, resource, and decision context for security review.
- Revocation: suspend or revoke agents, sessions, tokens, and delegations.

## What Bastion Is Not

Bastion is not trying to be a full Auth0, Clerk, Keycloak, Ory, or Zitadel replacement.

Those systems solve a broad and mature category and mainly focus on human centric auth with agent auth bolted on. Bastion starts with a sharper wedge: identity, delegated authority, and auditability for autonomous applications with AI agents.

Human authentication matters, but the first differentiated problem to solve today is agent authority.

## Design Principles

- Use existing standards before inventing new protocols.
- Treat agent credentials as high-risk secrets.
- Prefer short-lived, scoped, audience-bound access.
- Make delegation explicit and revocable.
- Preserve provenance: user, agent, client, resource, scopes, and time.
- Keep the core self-hostable.
- Document security tradeoffs honestly.
- Build small, reviewable milestones.

## Early Architecture

```text
Human user
    |
    | approves scoped delegation
    v
Bastion authorization server
    |
    | issues scoped, audience-bound token
    v
AI agent / agent runtime
    |
    | calls protected API, MCP server, or tool
    v
Resource server
    |
    | validates token, audience, scopes, and policy
    v
Audit log
```

The first Bastion milestone is a working end-to-end demo:

1. A user signs in.
2. An admin registers an agent.
3. The user delegates limited scopes to that agent.
4. The agent calls a protected resource.
5. Bastion records the full delegation and access path.
6. The agent can be suspended or revoked.

## Standards Direction

Bastion will track and use established identity/security work, including:

- OAuth 2.1 security practices.
- OpenID Connect discovery where useful.
- OAuth protected resource metadata for resource-server discovery.
- Dynamic client registration and client metadata where appropriate.
- PKCE for authorization-code flows.
- Audience-bound tokens to avoid token passthrough.
- MCP authorization requirements for protected MCP servers.

## Repository Layout

This repository starts with product, security, and contribution scaffolding before implementation:

```text
docs/
  architecture.md
  threat-model.md
examples/
  README.md
```

Implementation directories will be added as the first technical milestone is scoped.

## Roadmap

See [ROADMAP.md](ROADMAP.md).

The first release target is `v0.1.0-alpha`: a minimal but coherent demo of agent registration, delegated scopes, token issuance, protected-resource validation guidance, and audit logs.

## Contributing

Bastion development has just started. Early contributions are welcome, especially around:

- Threat modeling.
- OAuth/OIDC/MCP authorization review.
- Documentation clarity.
- Example apps and protected-resource demos.
- Tests for delegation edge cases.

Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

## Security

Auth and delegation infrastructure is security-sensitive. Do not open public issues for suspected vulnerabilities. See [SECURITY.md](SECURITY.md).

## License

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE).
