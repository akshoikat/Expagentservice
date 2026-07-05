PDS 01

docs/design/01-technology-stack.md

Version: 1.0

Status: Approved

1. Design Goals

Technology নির্বাচন করার সময় আমাদের priority হবে:

Stability
Long-term maintenance
Type safety
Strong ecosystem
Production readiness
Good developer experience
Easy deployment
Replaceability

Performance গুরুত্বপূর্ণ, কিন্তু readability ও maintainability-এর পরে।

2. High-Level Technology Map
Browser
    │
    ▼
Next.js (React)
    │
    ▼
Fastify API
    │
    ▼
Application Modules
    │
    ▼
AI Runtime
    │
    ▼
Infrastructure
3. Frontend
Framework

Next.js

Reason

Stable
App Router
React ecosystem
SSR
Good authentication support
UI
React
TypeScript
Styling

Tailwind CSS

Reason

Fast development
Small bundle
Large ecosystem
Icons

Lucide

State Management

Zustand

Reason

Simple
Minimal boilerplate
Excellent TypeScript support

Redux হবে না, কারণ V1-এর complexity-এর জন্য Zustand যথেষ্ট।

Server State

TanStack Query

Reason

API caching
Optimistic updates
Retry
Pagination
4. Backend
Runtime

Node.js LTS

Framework

Fastify

Reason

High performance
Plugin architecture
Excellent TypeScript support
ORM

Prisma

Reason

Migration support
Type safety
Excellent developer experience
Validation

Zod

Reason

একটি schema থেকে:

API validation
Type inference
Form validation

সব করা যাবে।

5. Database

Primary Database:

PostgreSQL

Reason:

ACID compliance
Mature ecosystem
JSONB support
Strong indexing
Reliable transactions
Cache

Redis

ব্যবহার হবে:

Session
Rate limiting
Queue support
Cache
Temporary context
Vector Search

Phase 1: pgvector

কারণ:

PostgreSQL-এর সাথে একই infrastructure।
Operational complexity কম।
V1-এর জন্য যথেষ্ট।

Future: Qdrant (যদি scale বা advanced vector features দরকার হয়)।

এটি আমাদের প্রথম simplification decision।

Object Storage

S3-compatible storage

লোকাল development:

MinIO

Production:

Cloudflare R2 / AWS S3
6. AI Runtime

Provider Interface থাকবে।

V1 Provider:

OpenAI

Future:

Claude
Gemini
Ollama
vLLM
Embeddings

শুরুতে OpenAI embeddings ব্যবহার করা হবে।

Provider abstraction থাকবে।

7. Background Processing

BullMQ

কেন Temporal না?

Temporal খুব শক্তিশালী, কিন্তু V1-এর জন্য operational complexity বেশি।

BullMQ যথেষ্ট:

Retry
Delay
Scheduling
Queue
Workers

ভবিষ্যতে abstraction রেখে Temporal-এ migrate করা সম্ভব।

8. Authentication

Better Auth

Reason:

Modern
TypeScript
Self-hostable
Session support
9. Real-Time Communication

V1:

Server-Sent Events (SSE)

কারণ:

Streaming AI response-এর জন্য যথেষ্ট।
WebSocket-এর তুলনায় infrastructure সহজ।

Future:

WebSocket (typing indicator, live collaboration ইত্যাদির জন্য)
10. Logging

Pino

কারণ:

Fast
Structured JSON logs
Fastify-এর সাথে ভালো integration
11. Testing
Vitest
Playwright

V1-এ Jest ব্যবহার করা হবে না।

12. Package Manager

pnpm

Reason:

Fast
Disk efficient
Monorepo support
13. Monorepo

Turborepo

Reason:

Build caching
Task orchestration
Large ecosystem
14. Docker

লোকাল development এবং production উভয়ের জন্য Docker Compose ব্যবহার করা হবে।

15. Technology Summary

| Layer           | Technology          |
| --------------- | ------------------- |
| Frontend        | Next.js + React     |
| Backend         | Fastify             |
| Language        | TypeScript          |
| ORM             | Prisma              |
| Database        | PostgreSQL          |
| Vector          | pgvector            |
| Cache           | Redis               |
| Queue           | BullMQ              |
| AI              | OpenAI              |
| Validation      | Zod                 |
| Auth            | Better Auth         |
| Storage         | S3 / MinIO          |
| Logging         | Pino                |
| Tests           | Vitest + Playwright |
| Monorepo        | Turborepo           |
| Package Manager | pnpm                |


Definition of Done

এই document complete ধরা হবে যদি:

প্রতিটি core technology নির্ধারিত হয়।
প্রতিটির নির্বাচন করার কারণ নথিভুক্ত থাকে।
Replaceability strategy নির্ধারিত থাকে।
V1 এবং future upgrade path স্পষ্ট থাকে।

