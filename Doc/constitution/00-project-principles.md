Project Principles

Version: 1.0

Status: Approved

1. Purpose

এই document-এর উদ্দেশ্য হলো project-এর engineering principles define করা। Architecture, database, API, AI agent, workflow, integration, deployment এবং future feature development—সবকিছু এই principles অনুসরণ করবে।

2. Engineering Philosophy

আমরা নিচের philosophy অনুসরণ করব।

2.1 Documentation First

কোনো feature implement করার আগে তার documentation, architecture এবং design approve হতে হবে।

Idea
    ↓
Documentation
    ↓
Architecture
    ↓
Implementation
    ↓
Testing
    ↓
Release

2.2 Architecture Before Code

কোনো module-এর code লেখার আগে তার architecture, interfaces, data flow এবং dependencies স্পষ্টভাবে define করতে হবে।

2.3 Production-Ready by Default

প্রতিটি implementation এমনভাবে লেখা হবে যেন সেটি production deployment-এর উপযোগী হয়।

Prototype বা throwaway code repository-তে রাখা হবে না।

2.4 Incremental Development

Project ছোট ছোট version-এ build হবে।

V1
↓

Testing
↓

V2
↓

Testing
↓

V3
↓

Testing

3. Single Source of Truth

একটি তথ্যের authoritative source একটিই হবে।

উদাহরণ:

User Profile → PostgreSQL
Active Session → Redis
Embeddings → Vector Database
Environment Configuration → Environment Variables
AI Prompt Template → Prompt Registry

একই তথ্য একাধিক জায়গায় business source হিসেবে রাখা যাবে না।

4. Modular Design

প্রতিটি module স্বাধীনভাবে maintain ও test করা যাবে।

উদাহরণ:

Authentication
Conversation
AI Agent
Workflow
Integrations
Analytics

এক module অন্য module-এর internal implementation জানবে না।

5. Loose Coupling

Modules interface-এর মাধ্যমে communicate করবে।

কোনো module অন্য module-এর database table বা internal code-এর উপর সরাসরি নির্ভর করবে না।

6. Event-Driven Architecture

Business event system-wide communication-এর ভিত্তি হবে।

উদাহরণ:

Message Received
Message Sent
Conversation Created
Agent Assigned
Booking Confirmed
Workflow Started
Workflow Completed

7. AI is a Service

AI logic business logic-এর সাথে hardcoded থাকবে না।

AI থাকবে abstraction layer-এর পিছনে।

Application

↓

AI Service

↓

Provider Adapter

↓

GPT
Claude
Gemini
vLLM

8. External Services Must Be Abstracted

WhatsApp, Meta, Gmail, Telegram, Stripe, Calendar—প্রতিটি integration adapter-এর মাধ্যমে যুক্ত হবে।

Application layer কখনও provider-specific implementation জানবে না।

9. Security by Default
Secrets code-এ থাকবে না।
Least privilege access অনুসরণ করা হবে।
Sensitive data encrypt করা হবে।
Authentication ছাড়া protected resource access করা যাবে না।
Audit trail সংরক্ষণ করা হবে।

10. Multi-Tenant First

Platform শুরু থেকেই multi-tenant হবে।

প্রতিটি Workspace-এর data logically isolated থাকবে।

11. Stateless Services

Application server local memory-র উপর নির্ভর করবে না।

Persistent state থাকবে:

PostgreSQL
Redis
Object Storage
Vector Database

12. Observability

প্রতিটি গুরুত্বপূর্ণ operation trace করা যাবে।

ন্যূনতমভাবে:

Logs
Metrics
Errors
Execution History
Audit Logs

13. Error Handling
Structured errors
Meaningful messages
Consistent error format
Centralized handling
Retry যেখানে প্রযোজ্য

14. Testing is Mandatory

প্রতিটি module-এর জন্য:

Unit Test
Integration Test

Critical workflow-এর জন্য:

End-to-End Test

15. No Temporary Hacks

Temporary code, TODO workaround, hardcoded credentials, hardcoded IDs বা duplicate implementation production branch-এ গ্রহণযোগ্য নয়।

16. Scalability

Architecture এমন হবে যাতে ভবিষ্যতে নতুন channel, agent, workflow বা AI provider যোগ করতে বড় refactor না লাগে।

17. Extensibility

প্রতিটি major feature plugin বা module হিসেবে extend করা যাবে।

যেমন:

New AI Provider
New Social Platform
New CRM
New Payment Gateway

18. Traceability

প্রতিটি feature-এর জন্য trace থাকবে:
Requirement
    ↓
Documentation
    ↓
Architecture
    ↓
Database
    ↓
API
    ↓
Implementation
    ↓
Testing

19. Versioning

Project semantic versioning অনুসরণ করবে।

Major.Minor.Patch

1.0.0
1.1.0
1.1.1
2.0.0

Breaking change হলে Major version বাড়বে।

20. Code Review Checklist

প্রতিটি feature merge করার আগে নিশ্চিত করতে হবে:

Architecture অনুসরণ করা হয়েছে।
Database migration সঠিক।
Tests pass করছে।
Logging আছে।
Error handling আছে।
Documentation update হয়েছে।
Security impact বিবেচনা করা হয়েছে।

যখনই বড় architectural decision আসবে—যেমন Workflow Engine, AI Runtime, Memory System বা Agent Framework—সেটা সরাসরি implement না করে আগে একটি RFC document তৈরি করা হবে।

প্রতিটি RFC-তে থাকবে:

সমস্যা কী?
সম্ভাব্য সমাধানগুলো কী?
কেন একটি সমাধান বেছে নেওয়া হচ্ছে?
এর সুবিধা ও সীমাবদ্ধতা কী?
ভবিষ্যতের উপর প্রভাব কী?

এতে বড় সিদ্ধান্তগুলো নথিভুক্ত থাকবে এবং পরে পরিবর্তনের প্রয়োজন হলে কারণগুলো পরিষ্কার থাকবে।


