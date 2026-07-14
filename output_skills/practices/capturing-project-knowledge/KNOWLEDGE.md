# Project knowledge

Project knowledge is the shared understanding of the business domain and the codebase — the knowledge that persists across features and that code alone cannot communicate.

It is alive; it evolves with the project. It is never a replica of the code.

The layout below is the default this skill applies. When a project already organizes its knowledge differently, follow the project's structure and map each type onto where that project keeps it.

## Business domain

Business rules, invariants, tacit knowledge, and flows. Written for everyone involved in the product — product managers, process owners, designers, and engineers. If someone outside engineering cannot understand a business rule, it does not belong here.

### Project-level knowledge (root CLAUDE.md)

What is true about this project's business domain across all modules. This file must stay short.

It includes the project's ubiquitous language — the canonical terms the team uses to talk about the domain — along with business rules and invariants that cross modules expressed in natural language, and a brief description of each module.

### Module-level knowledge (<module>/CLAUDE.md)

What is true about a specific module's business logic.

It includes a short description of the module's purpose, business rules and invariants expressed in natural language, and pointers to flows for detailed walkthroughs. When a section grows large and contains multiple examples, step-by-step processes, or concrete calculations, that is a sign it should be a flow — move it to flows/ and leave a pointer.

### Flows (<module>/flows/\*.md)

Deep-dives on specific business flows within a single module. One file per use case. Read on demand when working on that flow.

Each flow describes the business process it solves, expressed in domain language, along with business rules and invariants specific to the flow in natural language. When the flow involves a sequence of steps with conditional decisions, an ASCII diagram describes each step as a business action. Code references serve only as anchors to locate the implementation — never as a description of the behavior itself. Related flows at the same level or at a higher level are linked when they exist.

### Cross-module flows (.claude/flows/\*.md)

Deep-dives on business flows that cross modules. One file per use case. Read on demand when working on that flow.

Each flow describes the business process it solves, expressed in domain language, along with business rules and invariants that span multiple modules in natural language. When the flow involves a sequence of steps with conditional decisions, an ASCII diagram describes each step as a business action. Code references serve only as anchors to locate the implementation — never as a description of the behavior itself. Detailed module-level flows are linked when they exist.

## Codebase

How we write code in this project — universal, independent of business domain.

### Conventions (.claude/rules/conventions/\*.md)

Recurring patterns and deliberate choices that the team applies consistently across the project. Each convention captures the decision to use a pattern and where it should be applied. Code examples may illustrate how to apply it. If removing a convention would not change how the agent implements code, it does not belong here.
