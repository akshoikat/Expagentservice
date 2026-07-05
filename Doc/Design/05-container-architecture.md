PDS-05
docs/design/05-container-architecture.md

Version: 1.0
Status: Approved

Purpose

এই document C4 Model-এর Level 2 (Container Diagram) define করবে।

এখানে "Container" বলতে Docker container বোঝানো হচ্ছে না।

C4 অনুযায়ী Container হলো একটি deployable application বা runtime boundary।

High Level Architecture
                    ┌──────────────────────────────┐
                    │         Browser              │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                          apps/web (Next.js)
                                   │
                     HTTPS / WebSocket / SSE
                                   │
                                   ▼
                         apps/api (Fastify)
                                   │
         ┌───────────────┬──────────┴───────────────┐
         ▼               ▼                          ▼
 packages/core     providers/*                Event Queue
         │               │                          │
         │               │                          ▼
         │               │                 apps/worker
         │               │                          │
         └───────────────┼───────────────┬──────────┘
                         ▼               ▼
                  PostgreSQL          Redis
                         │
                         ▼
                   Object Storage
                         │
                         ▼
               External Providers
(OpenAI, WhatsApp, Meta, Telegram, Gmail ...)
Container 1
apps/web

Technology:

Next.js
React
TypeScript

Responsibilities:

Dashboard
Inbox UI
Blueprint Builder
Conversation View
Knowledge Management
Workspace Settings
Analytics

Will Never Do:

Business Logic
AI Execution
Database Access

সবকিছু API-এর মাধ্যমে হবে।

Container 2
apps/api

Technology:

Fastify
TypeScript

Responsibilities:

Authentication
REST API
Webhooks
AI Orchestration
Conversation Management
Blueprint Management
File Upload
Event Publishing

এটাই platform-এর primary backend।

Container 3
apps/worker

Responsibilities:

Queue Processing
Long Running Jobs
AI Background Tasks
Embedding Generation
Scheduled Tasks
Retry Logic
Import / Export

Worker stateless হবে।

যে কোনো সময় restart করা যাবে।

packages/core

এটা deployable container না।

এটা business engine।

Contains:

Identity

Workspace

Communication

Agent Runtime

Knowledge

Memory

Workflow

Administration
providers

Contains:

OpenAI

WhatsApp

Redis

BullMQ

Storage

Email

SMS

Core এগুলোর implementation জানবে না।

Database Layer

Primary Database

PostgreSQL

Stores:

Users
Conversations
Messages
Blueprints
Contacts
Audit Logs
Cache Layer
Redis

Stores:

Sessions
Streaming
Rate Limits
Temporary Context
Job Cache

Redis source of truth হবে না।

Object Storage
Cloudflare R2

Future compatible:

S3
MinIO

Stores:

Images
Audio
Documents
Attachments
Avatars
AI Providers

External.

Examples:

OpenAI
Claude
Gemini

সব Provider Adapter-এর মাধ্যমে connect হবে।

Communication Providers

Examples:

WhatsApp Business
Messenger
Instagram
Telegram
Gmail

সব Channel Gateway-তে normalize হবে।

Communication Matrix
Web → API

Protocol:

HTTPS

Streaming:

SSE (V1)

Future:

WebSocket

API → Worker

Protocol:

Queue

(BullMQ)

Worker → API

No direct call.

Worker event publish করবে।

API → Database

ORM

(Prisma)

API → Redis

Cache

API → OpenAI

Provider Layer

API → WhatsApp

Provider Layer

Sync vs Async
Sync
Login
Send Message
Open Conversation
Search
Blueprint CRUD
Async
AI Reply
Embeddings
Knowledge Processing
Media Processing
Analytics
Workflow Execution
Deployment Strategy

V1

apps/web

apps/api

apps/worker

একই server-এ deploy করা যাবে।

Future

apps/web

apps/api

apps/worker-ai

apps/worker-media

apps/worker-workflow

Worker split করা যাবে।

Container Rules

Web

↓

API only

Worker

↓

No UI

Core

↓

No Provider

Provider

↓

No Business Logic

Database

↓

No Business Rules

Failure Strategy

যদি AI Provider down হয়:

Worker retry করবে।

যদি WhatsApp down হয়:

Outgoing queue retry করবে।

যদি Redis down হয়:

System degraded mode-এ চলবে।

যদি Worker down হয়:

API চলবে।

Background job pause হবে।