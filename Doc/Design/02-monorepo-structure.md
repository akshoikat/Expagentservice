Design Goal

Repository এমন হবে যাতে:

নতুন developer ১০ মিনিটে structure বুঝতে পারে।
নতুন module যোগ করতে root structure পরিবর্তন করতে না হয়।
Core, Extensions এবং Providers আলাদা থাকে।
Documentation code-এর সাথে evolve করে।

Repository Layout

আমি root-কে যতটা সম্ভব ছোট রাখতে চাই।
ai-automation-platform/
│
├── apps/
├── packages/
├── providers/
├── docs/
├── docker/
├── scripts/
├── tools/
│
├── .github/
├── .vscode/
│
├── package.json
├── pnpm-workspace.yaml
├── turbo.json
├── tsconfig.base.json
├── .env.example
├── .gitignore
├── README.md
└── LICENSE

apps/

apps মানে runnable applications।

V1-এ:

apps/

web/
api/
worker/
web

Next.js Dashboard

api

Fastify Backend

worker

BullMQ Worker

Future-এ

Scheduler

AI Worker

Importer

Exporter

সব Worker-এর মধ্যেই আসতে পারবে।

packages/

এটাই আমাদের Core।

packages/

core/

shared/

sdk/

config/
core/

Platform business logic।

Future

core/

identity/

workspace/

communication/

agent/

workflow/

knowledge/

memory/

analytics/

এখানেই project-এর heart থাকবে।

shared/

Reusable code।

Examples

Types
Utils
Constants
Errors
sdk/

Internal SDK।

Frontend যেন Backend-এর types reuse করতে পারে।

config/

Shared Config

ESLint

TypeScript

Prettier

Environment Validation

providers/

এটা আমি আলাদা রাখতে চাই।

কারণ এগুলো Third-party implementation।

providers/

llm/

storage/

queue/

auth/

notification/

integration/

Example

providers/

llm/

openai/

providers/

queue/

bullmq/

Core কখনও provider import করবে না।

সবসময় interface import করবে।

docs/

এটা আমরা আগেই define করেছি।

docker/
docker/

development/

production/
scripts/

Development helper scripts।

tools/

Internal CLI

Migration

Generator

Seeder

Future Code Generator

Root Principle

Root-এ business code থাকবে না।

সব business code

apps/

বা

packages/

এ থাকবে।

V1 Implementation

V1-এ আসলে আমাদের দরকার:

apps/
    web/
    api/
    worker/

packages/
    core/
    shared/
    config/

providers/
    llm/
    queue/
    storage/

docs/
docker/
scripts/

অর্থাৎ এখনই ৫০টা folder বানাব না।

Future Extension

Future-এ

packages/

workflow/

knowledge/

analytics/

billing/

আলাদা package হতে পারে।

এখন দরকার নেই।

