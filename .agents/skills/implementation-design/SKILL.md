---
name: Implementation design
description: Apply architecture, SOLID, readability, simplicity, and test seams without speculative structure
---

# Implementation design

Judge design against the current requirements and the repository's established structure. Prefer the smallest design that stays understandable. Minimality means low conceptual cost, not the fewest lines.

## Responsibilities and boundaries

- Give a unit one reason to change at the code level that fits the problem. Keep behavior together when it changes for the same reason. Separate behavior when its reasons to change differ.
- Keep business policy independent of concrete databases, networks, filesystems, user interfaces, and framework details when a boundary creates a useful test or replacement seam.
- Shape contracts around what each consumer needs. Do not make callers depend on operations they do not use.
- Preserve the promised behavior of a shared contract across every implementation. Substitutability is behavioral and does not require inheritance.
- Apply open-closed guidance only when the repository already has demonstrated variation or stable policy that repeated edits would put at risk. Do not predict extension points.

Prefer composition and the language's ordinary dependency-injection tools. Functions, parameters, closures, modules, and data values are valid tools. Do not require classes, inheritance, or a formal ports-and-adapters layout.

## Architectural fit

Start with repository instructions and nearby code. Follow existing boundaries and conventions unless the requested behavior exposes a concrete defect in them. Introduce a boundary only when it addresses a current responsibility, external dependency, consumer contract, or tested variation.

Keep external dependencies replaceable at useful test seams. A seam is useful when tests or another current implementation need to control the dependency. Avoid wrappers that merely rename a library API.

## Readability and simplicity

- Optimize for the next maintainer's ability to understand behavior and change it safely.
- Reject compressed code when explicit control flow or naming is easier to read.
- Accept local repetition when no stable shared concept has emerged.
- Remove unnecessary dependencies, layers, indirection, configuration, and refactors.
- Do not create an abstraction based only on possible future use.

When implementing, state the current reason for each new abstraction. When reviewing, do not cite a design principle as a defect by itself. Identify the concrete evidence and the effect on correctness, change cost, testing, or readability.

## Tests

Test through the highest useful public seam. Verify observable behavior instead of private methods or incidental call order. Use integration tests at meaningful boundaries and focused unit tests where isolation improves determinism or diagnosis. Use fakes for external systems when they make tests deterministic, and real integrations when the integration contract or configuration is the behavior under test.
