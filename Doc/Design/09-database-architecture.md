PDS-09
docs/design/09-database-architecture.md

এটা হবে Database-এর constitution।

এখানে কোনো table define করা হবে না।

শুধু rules define হবে।

1. Database Philosophy

Platform uses a hybrid persistence architecture.

Different kinds of data have different storage requirements.

We will choose storage based on data characteristics, not convenience.

2. Storage Strategy
                    Application
                          │
      ┌───────────────────┼───────────────────┐
      ▼                   ▼                   ▼
 PostgreSQL           Redis              Object Storage
      │                   │                   │
      ▼                   ▼                   ▼
 Business Data      Cache & Runtime     Files & Media
                          │
                          ▼
                     Vector Store
                    (pgvector V1)
3. Source of Truth

Only PostgreSQL is the authoritative source of business data.

Redis is never a source of truth.

Vector storage can always be rebuilt.

Runtime cache is disposable.

4. Data Classification

আমি সব data-কে ৬টি category-তে ভাগ করতে চাই।

Business Data

Runtime Data

AI Data

Infrastructure Data

Operational Data

Analytical Data
Business Data

Examples:

Users
Workspaces
Contacts
Conversations
Blueprints

Highest consistency required.

Runtime Data

Examples:

Active Sessions
Queue Status
Streaming State
Temporary Context

Disposable.

AI Data

Examples:

Memories
Embeddings
Chunks
Summaries

Regenerable.

Infrastructure Data

Examples:

OAuth Tokens
Provider Credentials
Webhook Metadata

Sensitive.

Operational Data

Examples:

Job History
Retry Records
Health Checks
Delivery Logs

Used for operations.

Analytical Data

Examples:

Token Usage
Reports
Metrics
Audit Logs

Append-heavy.

5. Ownership Rule

Every table has exactly one owner.

Only the owning module defines write rules.

Other modules interact through services, repositories, or events.

6. Workspace Isolation

Every tenant-owned entity must contain:

workspace_id

Exception:

Platform users
Global roles
System configuration
7. Global Entity Rule

Only platform-level entities are allowed without workspace ownership.

Examples:

countries

languages

system_settings

feature_flags

Everything else belongs to a workspace.

8. Soft Delete Policy

Soft delete only where business recovery matters.

Examples:

Yes:

Contacts
Conversations
Blueprints
Documents

No:

Cache
Embeddings
Temporary Sessions
Queue Jobs
9. Audit Strategy

Critical business entities must support auditing.

Examples:

Blueprint Published
Conversation Assigned
Workspace Member Removed
Policy Updated
10. Versioning Policy

Versioning only for immutable business artifacts.

Examples:

Versioned:

Blueprints
Workflows
Policies
Knowledge Collections

Not Versioned:

Messages
Contacts
Runtime Sessions
11. Storage Selection Matrix
Business Entity
        │
        ▼
PostgreSQL

--------------

Temporary Runtime
        │
        ▼
Redis

--------------

Large File
        │
        ▼
Object Storage

--------------

Semantic Search
        │
        ▼
pgvector (V1)

--------------

Analytics
        │
        ▼
PostgreSQL
12. Database Design Principles
Normalize business data.
Denormalize only for measured performance needs.
Every FK must express business ownership.
Avoid polymorphic relationships where possible.
Prefer explicit junction tables over hidden relationships.
Every schema change requires an ADR or migration note.

ADR-0018 — Ownership-First Database Architecture

Decision

The database will be designed from business ownership rather than from table relationships.

Storage technology will be selected according to data characteristics.

Business modules own data.

Execution engines consume data.

Infrastructure stores implementation details.

