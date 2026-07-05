PDS-06
docs/design/06-domain-model.md

Version: 1.0
Status: Draft → Approved after review

Purpose

এই document define করবে:

Core Business Entities
Aggregate Boundaries
Ownership
Relationships
Lifecycle

Rule:

Database table পরে আসবে। আগে business entity define হবে।

Platform Root
Platform
│
└── Workspace
      │
      ├── Members
      ├── Blueprints
      ├── Channels
      ├── Contacts
      ├── Conversations
      ├── Knowledge Bases
      └── Workflows

Workspace হবে পুরো platform-এর root business boundary।

এটার মানে:

সব data workspace-scoped হবে।
Multi-tenant support naturally আসবে।
Data isolation সহজ হবে।
Aggregate 1 — Workspace
Owns
Workspace
WorkspaceSettings
WorkspaceMember
WorkspaceRole
Responsibilities
Tenant boundary
Access control
Feature enablement
Configuration
Aggregate 2 — Blueprint

এটাই platform-এর heart।

Blueprint
│
├── Persona
├── Instructions
├── KnowledgeBindings
├── ToolBindings
├── WorkflowBindings
├── PolicyBindings
├── MemoryProfile
├── ModelProfile
└── ChannelBindings

Blueprint কখনও conversation store করবে না।

Blueprint শুধু behavior define করবে।

Aggregate 3 — Conversation
Conversation
│
├── Contact
├── Messages
├── Assignments
├── Labels
├── Timeline
└── State

Conversation হলো execution context।

Aggregate 4 — Contact
Contact
│
├── Identity
├── Profile
├── Channels
├── Tags
├── Preferences
└── Custom Fields

একজন Contact-এর একাধিক channel থাকতে পারে।

উদাহরণ:

WhatsApp
Messenger
Instagram

কিন্তু business entity থাকবে একটাই Contact।

Aggregate 5 — Knowledge Base
Knowledge Base
│
├── Documents
├── Chunks
├── Embeddings
├── Sources
└── Index

Blueprint knowledge bind করবে।

Knowledge Blueprint-এর অংশ হবে না।

Aggregate 6 — Workflow
Workflow
│
├── Nodes
├── Connections
├── Variables
├── Triggers
└── Actions

Workflow reusable হবে।

একটি Workflow বহু Blueprint ব্যবহার করতে পারবে।

Aggregate 7 — Integration
Integration
│
├── Provider
├── Credentials
├── Configuration
├── Status
└── Permissions

WhatsApp connection এখানে থাকবে।

Conversation-এ নয়।

Aggregate 8 — Agent Instance

এখানে আগের discussion-এর continuation।

Blueprint

↓

Deployment

↓

Agent Instance

Instance owns:

Runtime State
Execution Metrics
Health
Current Sessions

Blueprint immutable হতে পারে।

Instance mutable হবে।

Aggregate Relationships
Workspace
│
├── Blueprints
├── Contacts
├── Conversations
├── Knowledge Bases
├── Workflows
├── Integrations
└── Members

Blueprint
│
├── uses Persona
├── uses Workflow
├── uses Knowledge
├── uses Policies
└── deploys Agent Instance

Conversation
│
├── belongs to Contact
├── executed by Agent Instance
└── produces Memory
Ownership Rules

Workspace owns:

Members
Roles

Blueprint owns:

Behavior

Conversation owns:

Messages

Knowledge owns:

Documents

Workflow owns:

Nodes

Integration owns:

Credentials
Forbidden Ownership

Conversation কখনও Persona own করবে না।

Blueprint কখনও Message own করবে না।

Workflow কখনও Contact own করবে না।

Knowledge কখনও Conversation own করবে না।

এই rule future complexity কমাবে।

Lifecycle Example
Workspace Created
        │
        ▼
Blueprint Created
        │
        ▼
Blueprint Published
        │
        ▼
Blueprint Deployed
        │
        ▼
Agent Instance Running
        │
        ▼
Customer Starts Conversation
        │
        ▼
Conversation Executes
        │
        ▼
Memory Updated