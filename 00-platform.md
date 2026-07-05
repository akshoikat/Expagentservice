প্রতিটি Entity Datasheet-এর আগে একটি Aggregate Datasheet থাকবে।

DDD (Domain-Driven Design)-এ Entity একা থাকে না। Entity সবসময় Aggregate-এর ভিতরে থাকে।

উদাহরণ:

Platform
│
├── Workspace Aggregate
│   ├── Workspace
│   ├── WorkspaceMember
│   ├── WorkspaceRole
│   └── WorkspaceSettings
│
├── Blueprint Aggregate
│   ├── Blueprint
│   ├── BlueprintVersion
│   ├── Deployment
│   └── AgentInstance
│
├── Communication Aggregate
│   ├── Contact
│   ├── Conversation
│   ├── Message
│   └── TimelineEvent
│
├── Knowledge Aggregate
│   ├── KnowledgeBase
│   ├── Document
│   ├── Chunk
│   └── Embedding
│
├── Workflow Aggregate
│   ├── Workflow
│   ├── WorkflowVersion
│   ├── WorkflowExecution
│   └── WorkflowVariable
│
└── Integration Aggregate
    ├── Integration
    ├── Credential
    ├── Webhook
    └── ProviderAccount

এতে একটা বড় সুবিধা হবে।

যখন আমরা Conversation লিখব, তখন আগে থেকেই জানা থাকবে:

এর owner aggregate কে?
কোন entity root?
কোন entity বাইরে expose হবে?
কোন entity internal?
আমি documentation structure-টা এভাবে lock করতে চাই
docs/
│
├── constitution/
│
├── architecture/
│
├── adr/
│
├── domain/
│   │
│   ├── 00-platform.md
│   │
│   ├── aggregates/
│   │   ├── workspace.md
│   │   ├── blueprint.md
│   │   ├── communication.md
│   │   ├── knowledge.md
│   │   ├── workflow.md
│   │   └── integration.md
│   │
│   └── entities/
│       ├── workspace.md
│       ├── workspace-member.md
│       ├── blueprint.md
│       ├── blueprint-version.md
│       ├── deployment.md
│       ├── contact.md
│       ├── conversation.md
│       ├── message.md
│       ├── memory.md
│       ├── workflow.md
│       └── ...
│
├── database/
│
└── api/
এরপর আমি Platform Datasheet দিয়ে শুরু করব।

এটা কোনো database entity নয়।

এটা পুরো system-এর root specification।

DDS-000
docs/domain/00-platform.md

Version: 1.0
Status: Approved

Purpose

The Platform is the highest-level business boundary of the system.

It defines global rules, ownership hierarchy, tenant isolation, runtime architecture, and the contracts that every module must follow.

The Platform itself is not a database entity.

It is a conceptual root that governs all business entities.

Mission

Provide a unified, blueprint-driven AI automation platform capable of running multiple professional AI roles through a shared execution runtime.

The platform must support:

AI Customer Support
WhatsApp Automation
Social Media Management
Hotel Reception
Medical Reception
Booking Automation
CRM Automation
Future AI roles without runtime changes
Core Philosophy

Separate business definition from execution.

Business is expressed through Blueprints.

Execution is performed by Runtime Engines.

Infrastructure remains replaceable.

Ownership Hierarchy
Platform
│
└── Workspace
    │
    ├── Members
    ├── Blueprints
    ├── Contacts
    ├── Conversations
    ├── Knowledge Bases
    ├── Workflows
    ├── Integrations
    └── Analytics

Everything belongs to exactly one Workspace unless explicitly defined as a global platform resource.

Core Business Objects

The platform is composed of seven primary business objects:

Workspace
Blueprint
Agent Instance
Conversation
Knowledge Base
Workflow
Integration

Every other entity exists to support one of these objects.

Runtime Model
Blueprint
      │
      ▼
Deployment
      │
      ▼
Agent Instance
      │
      ▼
Conversation
      │
      ▼
Execution Engines
      │
      ▼
External Providers
Execution Model

Business Definition:

Blueprint
Persona
Policies
Knowledge
Workflow

Execution:

Conversation Engine
Memory Engine
Tool Engine
Knowledge Engine
Channel Engine

Storage:

PostgreSQL
Redis
Object Storage
Vector Store
Global Design Principles
Workspace-first ownership.
Blueprint-driven behavior.
Engine-based execution.
Provider abstraction.
Event-oriented communication.
Explicit lifecycle management.
Module ownership.
Replaceable infrastructure.
Contract-first implementation.
Cross-Cutting Concerns

Every module must support, where applicable:

Authentication
Authorization
Audit Logging
Observability
Versioning
Soft Delete
Validation
Metrics
Feature Flags

These concerns are implemented consistently across the platform rather than individually by each module.

Naming Standards
Business entities use singular names (Workspace, Conversation).
Database tables use plural names (workspaces, conversations).
Modules use singular domain names (Communication, Blueprint).
Engines use the <Domain> Engine pattern (Memory Engine, Tool Engine).
Architectural Constraints

The platform must never:

Embed business logic inside provider adapters.
Embed provider-specific logic inside runtime engines.
Couple Blueprints to infrastructure.
Allow one module to write another module's business data directly.
Use infrastructure details as business contracts.
Success Criteria

The platform is considered architecturally successful when:

A new professional AI role can be introduced by creating a Blueprint rather than writing a new runtime.
Infrastructure providers can be replaced without changing business logic.
Business modules remain independently testable.
Runtime engines remain reusable across domains.
Multi-tenant isolation is enforced by design.
ADR-0019 — Platform as a Conceptual Root

Decision

The Platform is defined as a conceptual domain root rather than a persistent entity.

All business entities derive their ownership and architectural constraints from the Platform specification.p[mn ]