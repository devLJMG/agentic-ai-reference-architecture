# ADR-001: Ports-and-adapters for the agent runtime

- Status: Accepted
- Date: 2026-09-02

## Context

The reference implementation needs to demonstrate Amazon Bedrock, retrieval, memory and external tools without tightly coupling orchestration logic to individual AWS SDK calls.

Agentic applications are especially sensitive to coupling because model providers, retrieval mechanisms, memory implementations and tools evolve independently.

## Decision

The runtime will use a ports-and-adapters approach.

The orchestrator depends on explicit interfaces for:

- model invocation;
- retrieval;
- memory;
- tool execution;
- telemetry.

AWS-specific implementations will live behind these interfaces.

## Consequences

### Positive

- Core orchestration can be unit-tested without AWS credentials.
- Infrastructure dependencies remain visible.
- Bedrock or retrieval implementations can evolve independently.
- Tool authorization can be enforced outside model reasoning.
- The repository demonstrates software architecture rather than only SDK usage.

### Trade-offs

- More interfaces and files than a minimal prototype.
- Additional mapping between domain objects and AWS SDK payloads.
- Developers must resist bypassing ports for convenience.

## Rejected alternative

Directly invoking AWS SDK clients throughout the orchestration code was rejected because it would make tests harder, increase coupling and blur the boundary between reasoning and infrastructure execution.
