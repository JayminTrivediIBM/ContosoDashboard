<!--
Sync Impact Report
- Version change: 0.0.0 → 1.0.0
- Modified principles: none (initial constitution)
- Added sections: Additional Constraints, Development Workflow
- Removed sections: none
- Templates requiring updates: ✅ .specify/templates/plan-template.md (no change required), ✅ .specify/templates/spec-template.md (no change required), ✅ .specify/templates/tasks-template.md (no change required)
- Follow-up TODOs: none
-->

# ContosoDashboard Constitution

## Core Principles

### I. Training-First Scope
All work in this repository MUST preserve its role as a training sample for Spec-Driven Development. Features MUST be understandable, intentionally simplified, and suitable for learning. Code MUST NOT imply production readiness or claim production support. When a decision adds complexity without teaching a clear concept, the simpler option MUST be preferred.

### II. Security by Default
Every change affecting authentication, authorization, data access, or user-visible routes MUST preserve the existing defense-in-depth model. Protected pages MUST require authorization, service methods MUST enforce access rules, and user data MUST remain isolated by identity. New features MUST NOT introduce bypasses, privilege escalation, or unsafe direct object access.

### III. Offline-First and Portable Architecture
The application MUST remain runnable in a local offline training environment without external services. New features SHOULD use dependency injection and clear abstraction boundaries so local implementations can be swapped for cloud implementations later. Changes MUST NOT introduce hard dependencies on hosted services unless explicitly documented as out of scope for this training project.

### IV. Testable and Verifiable Changes
Work MUST be verifiable through build, runtime, or manual validation steps. Features affecting behavior MUST include explicit validation steps, and changes to security, routing, or persistence MUST be demonstrated with a concrete scenario. If a requirement cannot be tested, it MUST be clarified before implementation.

### V. Simplicity and Documentation
Implementation choices MUST favor clear, maintainable code over premature abstraction. New functionality MUST include enough documentation or inline guidance for learners to understand the intent, tradeoffs, and relevant files. Complex decisions MUST be justified in design notes or comments rather than hidden in implementation.

## Additional Constraints
The project MUST remain aligned with the current stack: ASP.NET Core with Blazor Server, EF Core, and local development data. The application MUST continue to use mock authentication for training scenarios; production-grade identity providers are out of scope unless explicitly introduced as a separate feature branch. Data and file operations MUST remain local-first; any new storage or integration work MUST be isolated behind abstractions and documented as optional. Features MUST avoid introducing breaking changes to the existing navigation, page contracts, or authentication flows unless the specification explicitly calls for them.

## Development Workflow
Every feature MUST start from a concrete specification with user scenarios, acceptance criteria, and measurable outcomes. Implementation MUST follow a verification-first workflow: build or test validation MUST occur before considering the work complete. Security-sensitive and access-control changes MUST be reviewed for authorization, data isolation, and regression risk. Documentation updates MUST accompany behavior changes that affect how learners run, test, or understand the app.

## Governance
This constitution supersedes informal project practices for this repository. Any amendment MUST be documented in this file, include a version bump, and describe the rationale for the change. Changes that alter core principles or security expectations MUST be reviewed before implementation proceeds. Compliance with this constitution is evaluated during planning, implementation review, and release readiness.

**Version**: 1.0.0 | **Ratified**: 2026-07-01 | **Last Amended**: 2026-07-01
