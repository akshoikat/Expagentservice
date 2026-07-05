PDS-03

docs/design/03-module-boundaries.md

Purpose

প্রতিটি Module-এর:

Responsibility
Ownership
Public API
Internal API
Dependencies
Events
Database Ownership

স্পষ্টভাবে define করা।

Rule:

One Module = One Business Capability

Platform Module Map
AI Automation Platform
│
├── Identity
├── Workspace
├── Communication
├── Agent Runtime
├── Knowledge
├── Memory
├── Workflow
├── Integration Hub
├── Notification
├── Analytics
├── Billing
└── Administration
Module 1
Identity
Responsibility

Platform Identity Management

Owns
User

Role

Permission

Session

API Key
Public API
Create User

Login

Logout

Validate Session

Check Permission
Publishes
UserCreated

UserLoggedIn

UserLoggedOut

RoleAssigned
Consumes

Nothing

Module 2
Workspace
Responsibility

Tenant Management

Owns
Workspace

WorkspaceMember

WorkspaceSettings
Public API
Create Workspace

Invite Member

Remove Member

Update Settings
Publishes
WorkspaceCreated

MemberInvited

MemberRemoved
Depends On

Identity

Module 3
Communication

এটাই V1-এর Core Module।

Owns
Channel

Contact

Conversation

Message

Inbox

Assignment

Label
Public API
Create Conversation

Send Message

Receive Message

Assign Conversation

Archive Conversation
Publishes
ConversationCreated

MessageReceived

MessageSent

ConversationAssigned

ConversationClosed
Consumes
UserLoggedIn

WorkspaceCreated
Depends On

Workspace

Identity

Module 4
Agent Runtime
Owns
Agent

Persona

Prompt

Tool Registry

AI Session
Public API
Execute Agent

Generate Reply

Run Tool

Build Context
Publishes
AgentExecuted

ToolCalled

ReplyGenerated
Consumes
MessageReceived
Depends On

Communication

Knowledge

Memory

Module 5
Knowledge
Owns
Document

Source

Embedding

Retriever
Public API
Upload Document

Delete Document

Search Knowledge
Publishes
KnowledgeUpdated
Module 6
Memory
Owns
Memory

Memory Event

Summary
Public API
Store Memory

Retrieve Memory

Summarize Conversation
Publishes
MemoryUpdated
Consumes
ConversationClosed

ReplyGenerated
Module 7
Workflow
Owns
Workflow

Node

Execution

Trigger

Action
Public API
Start Workflow

Stop Workflow

Execute Node
Publishes
WorkflowStarted

WorkflowCompleted

WorkflowFailed
Module 8
Integration Hub
Owns
Integration

Credential

Webhook

Provider
Public API
Connect Provider

Disconnect Provider

Verify Connection
Publishes
IntegrationConnected

WebhookReceived
Module 9
Notification
Owns
Notification

Template
Module 10
Analytics
Owns
Metrics

Usage

Reports
Module 11
Billing
Owns
Subscription

Invoice

Payment
Module 12
Administration
Owns
Audit Log

Feature Flag

Platform Settings
Dependency Rules

সবচেয়ে গুরুত্বপূর্ণ অংশ।

Identity
        │
        ▼
Workspace
        │
        ▼
Communication
        │
   ┌────┼─────────┐
   ▼    ▼         ▼
Agent Workflow Integration
   │      │
   ├──┬───┘
   ▼  ▼
Knowledge Memory
        │
        ▼
Analytics
Forbidden Dependencies
Knowledge → Identity ❌

Memory → Workspace ❌

Workflow → PostgreSQL ❌

Agent → WhatsApp API ❌

Communication → OpenAI SDK ❌

সব provider access Integration বা Provider layer দিয়ে হবে।

Module Ownership Rule

একটি Entity-এর Owner মাত্র একটি Module।

উদাহরণ:

Conversation

Owner:
Communication

NOT

Workflow

NOT

Agent

Workflow Conversation ব্যবহার করতে পারবে।

Owner হবে না।

Database Ownership

এটাও এখন define করে ফেলি।

Identity

↓

users

roles

sessions

-------------------

Communication

↓

contacts

conversations

messages

-------------------

Knowledge

↓

documents

embeddings

-------------------

Memory

↓

memory_events

summaries

-------------------

Workflow

↓

workflows

workflow_nodes

executions

একটি table-এর Owner একটি Module।

V1 Modules

V1-এ implement হবে:

Identity

Workspace

Communication

Agent Runtime

Knowledge

Memory

Integration

Administration

V2

Workflow

Analytics

Notification

V3

Billing

Marketplace

Plugins