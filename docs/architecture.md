# Architecture

This document describes the intended early architecture for Bastion. It will evolve as implementation begins.

## Core Concepts

### Principal

An entity that can be identified in the system.

Initial principal types:

- user
- agent

### Agent

An AI agent, agent runtime, or agentic application component that can request delegated access.

An agent should have:

- stable ID
- display name
- owner or registering administrator
- lifecycle status
- allowed scope ceiling
- metadata for model/runtime/version/capabilities
- associated client credentials or client metadata

### Delegation

A user's explicit grant allowing an agent to act with limited authority.

A delegation should include:

- delegating user
- agent
- approved scopes
- resource or audience
- expiry
- revocation status
- timestamps
- audit context

### Effective Scope

The final set of permissions available to the agent.

```text
effective_scope = requested_scope intersected with agent_allowed_scope intersected with user_delegated_scope intersected with resource_policy
```

If any layer refuses the request, access should fail closed.

### Audit Event

A structured record of a security-relevant action.

Important audit fields:

- request ID
- event type
- actor type
- user ID, if present
- agent ID, if present
- client ID, if present
- delegation ID, if present
- resource/audience
- scopes
- decision
- reason
- timestamp


## Initial Flow

```text
Admin registers agent
    |
    v
Bastion stores agent with scope ceiling
    |
    v
User approves delegation to agent
    |
    v
Bastion issues scoped token for target resource
    |
    v
Agent calls protected resource
    |
    v
Resource validates issuer, audience, expiry, scopes
    |
    v
Bastion/resource emits audit event
```

## Token Direction

Access tokens should be:

- short lived
- scoped
- audience bound
- issuer validated
- connected to both user and agent context where applicable

The resource server must reject tokens that are not intended for it.

## Revocation Direction

Revocation should be possible at multiple levels:

- agent suspended or revoked
- delegation revoked
- client credential rotated
- session revoked
- refresh token revoked

The revocation model should be documented before any production-readiness claim.

## Open Design Questions

- Exact token claim names for user, agent, delegation, and provenance.
- Whether Bastion should issue JWTs only, opaque tokens only, or support both.
- How resource policy should be represented in the first release.
- How much MCP-specific discovery support belongs in the core versus examples.
- Whether agent metadata should follow a future standard profile.
