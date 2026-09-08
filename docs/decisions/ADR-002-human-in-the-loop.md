# ADR-002: Human approval for high-impact agent actions

- Status: Accepted
- Date: 2026-09-07

## Context

Agentic systems may call tools that create side effects. Model reasoning is probabilistic and cannot be treated as an authorization mechanism.

Some operations have sufficiently high impact that execution should require explicit approval even when the caller is authenticated and the agent has produced a valid plan.

## Decision

The architecture will include a policy-driven human-in-the-loop checkpoint between planning and execution for operations classified above a configurable risk threshold.

The model may propose an action, but deterministic policy code decides whether the proposal can execute automatically, must be rejected, or requires human approval.

## Approval payload

Approval requests should contain:

- correlation ID;
- requesting identity;
- proposed tool and operation;
- normalized parameters;
- model/orchestrator rationale summary;
- expected side effects;
- required permission scope;
- risk classification;
- expiration timestamp.

## Consequences

### Positive

- Separates model reasoning from execution authority.
- Reduces risk from prompt injection or incorrect planning.
- Provides a clear audit trail for sensitive operations.
- Supports enterprise governance and compliance requirements.

### Trade-offs

- Increases latency for high-risk actions.
- Requires an approval workflow and durable state.
- Policies and risk classifications must be maintained independently from prompts.

## Rejected alternative

Allowing the LLM or specialist agent to decide autonomously whether an operation is safe was rejected because the same probabilistic component proposing an action should not be its final authorization authority.
