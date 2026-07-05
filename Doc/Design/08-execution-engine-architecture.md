PDS-08

docs/design/08-execution-engine-architecture.md

Philosophy

Blueprint কী করবে তা define করে।

Engine কীভাবে করবে তা execute করে।

এই দুইটি কখনও একসাথে merge হবে না।

Core Model
Blueprint
        │
        ▼
Execution Engine
        │
        ▼
Runtime State
        │
        ▼
Result

Blueprint declarative।

Engine imperative।

Engine Catalog

V1-এ:

Conversation Engine
Blueprint Engine
Memory Engine
Knowledge Engine
Tool Engine
Channel Engine
Integration Engine

Future:

Workflow Engine
Notification Engine
Analytics Engine
Voice Engine
Vision Engine
Multi-Agent Engine
Conversation Engine
Responsibility
Conversation lifecycle
State transitions
Context loading
Message routing
Human handoff
Session management

Input:

Incoming Message

Output:

Conversation Context
Blueprint Engine
Responsibility
Blueprint loading
Version resolution
Deployment resolution
Configuration merging
Runtime configuration

Input:

Blueprint ID

Output:

Resolved Runtime Configuration
Memory Engine
Responsibility
Memory scoring
Memory storage
Semantic retrieval
Summarization
Context optimization

Input:

Conversation

Output:

Relevant Memories
Knowledge Engine
Responsibility
Search
Retrieval
Ranking
Chunk selection
Citation generation

Input:

User Query

Output:

Knowledge Context
Tool Engine
Responsibility
Tool discovery
Permission checking
Parameter validation
Tool execution
Retry
Result normalization

Input:

Tool Request

Output:

Tool Result
Channel Engine
Responsibility
Provider normalization
Canonical message creation
Message delivery
Delivery status
Retry
Idempotency

Input:

Provider Payload

Output:

Canonical Message
Integration Engine
Responsibility
Provider lifecycle
Credential management
Health checks
Connection validation
Rate limiting
Capability discovery
Engine Interaction
Incoming Message
        │
        ▼
Channel Engine
        │
        ▼
Conversation Engine
        │
        ▼
Blueprint Engine
        │
        ├───────────────┐
        ▼               ▼
Memory Engine    Knowledge Engine
        │               │
        └──────┬────────┘
               ▼
         Runtime Context
               │
               ▼
             LLM
               │
        Need Tool?
               │
        ┌──────┴──────┐
        ▼             ▼
      No         Tool Engine
        │             │
        └──────┬──────┘
               ▼
      Conversation Engine
               │
               ▼
       Channel Engine
Engine Rules

সব Engine:

Stateless
Replaceable
Independently Testable
Observable
Provider Independent
Engine Communication

Engine কখনও database table access করবে না।

Engine Repository Interface ব্যবহার করবে।

Engine কখনও OpenAI SDK import করবে না।

Provider abstraction ব্যবহার করবে।

Engine কখনও অন্য Engine-এর internal state access করবে না।

শুধু Public Contract।

Engine Ownership

Conversation Engine

↓

Conversation Runtime

Memory Engine

↓

Memory Lifecycle

Knowledge Engine

↓

Knowledge Retrieval

Tool Engine

↓

Tool Execution

Blueprint Engine

↓

Blueprint Resolution

Channel Engine

↓

Communication Lifecycle