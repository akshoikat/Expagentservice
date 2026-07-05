PDS-07
docs/design/07-runtime-lifecycle.md

Version: 1.0
Status: Draft

Purpose

এই document define করবে:

Runtime কীভাবে শুরু হবে
Blueprint কীভাবে deploy হবে
Conversation কীভাবে execute হবে
Memory কখন update হবে
Tool কখন call হবে
Failure হলে কী হবে

Rule:

Everything in the platform is a lifecycle.

Static entity খুব কম।

Runtime Lifecycle Overview
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
Execution Cycle
      │
      ▼
Memory Update
      │
      ▼
Analytics
Lifecycle 1 — Blueprint
Draft
   │
   ▼
Validated
   │
   ▼
Published
   │
   ▼
Deployed
   │
   ▼
Archived

Rules

Draft edit করা যাবে।
Published immutable।
Deploy শুধু Published version থেকে।
Rollback supported।
Lifecycle 2 — Agent Instance
Created
    │
    ▼
Initializing
    │
    ▼
Ready
    │
    ▼
Running
    │
    ▼
Paused
    │
    ▼
Stopped

Ready মানে:

Provider connected
Blueprint loaded
Knowledge mounted
Tools initialized
Lifecycle 3 — Conversation
New
 │
 ▼
Received
 │
 ▼
Context Loaded
 │
 ▼
AI Processing
 │
 ├────────────┐
 ▼            ▼
Tool Call   Human Handoff
 │            │
 └────┬───────┘
      ▼
Reply Generated
      │
      ▼
Waiting Customer
      │
      ▼
Resolved
      │
      ▼
Closed
Lifecycle 4 — Tool Execution
Requested
      │
      ▼
Authorized
      │
      ▼
Executing
      │
      ▼
Succeeded

or

Failed
      │
      ▼
Retry

সব Tool একই lifecycle অনুসরণ করবে।

Lifecycle 5 — Knowledge
Uploaded
      │
      ▼
Validated
      │
      ▼
Chunked
      │
      ▼
Embedded
      │
      ▼
Indexed
      │
      ▼
Available
Lifecycle 6 — Memory
Conversation Event
        │
        ▼
Candidate Memory
        │
        ▼
Scored
        │
        ▼
Stored
        │
        ▼
Embedded
        │
        ▼
Searchable

সব message memory হবে না।

Importance score-এর ভিত্তিতে memory তৈরি হবে।

Lifecycle 7 — Human Handoff
AI
 │
 ▼
Need Human?
 │
 ├──────────┐
 │          │
No         Yes
 │          │
 ▼          ▼
Reply    Queue
            │
            ▼
Assigned
            │
            ▼
Operator
            │
            ▼
Resolved
            │
            ▼
AI Resume

AI conversation resume করতে পারবে।

Lifecycle 8 — Integration
Disconnected
      │
      ▼
Connecting
      │
      ▼
Connected
      │
      ▼
Verifying
      │
      ▼
Healthy

or

Failed
Lifecycle 9 — Worker Job
Queued
    │
    ▼
Running
    │
    ▼
Completed

or

Failed
    │
    ▼
Retry
    │
    ▼
Dead Letter

সব background task একই pattern অনুসরণ করবে।

Runtime Execution Cycle
Incoming Message
        │
        ▼
Normalize
        │
        ▼
Conversation Lookup
        │
        ▼
Load Blueprint
        │
        ▼
Load Memory
        │
        ▼
Search Knowledge
        │
        ▼
Build Context
        │
        ▼
LLM
        │
        ▼
Need Tool?
        │
 ┌──────┴──────┐
 │             │
No            Yes
 │             │
 ▼             ▼
Reply      Tool Engine
 │             │
 └──────┬──────┘
        ▼
Store Memory
        │
        ▼
Send Response

এটাই V1-এর primary execution loop।

Failure Recovery

যদি:

OpenAI fail করে → Retry → Fallback Model (Future)
WhatsApp fail করে → Queue Retry
Worker crash করে → Resume Job
Redis fail করে → Degraded Mode
Database fail করে → Read-only Protection (Future)
Runtime Rules
Blueprint কখনও runtime state store করবে না।
Conversation কখনও provider payload store করবে না।
Memory asynchronous হবে।
Analytics asynchronous হবে।
Embedding asynchronous হবে।
Media processing asynchronous হবে।