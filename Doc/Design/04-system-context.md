docs/design/04-system-context.md

Version: 1.0
Status: Approved

Purpose

এই document-এর উদ্দেশ্য হলো পুরো platform-এর system boundary নির্ধারণ করা।

এখানে আমরা code বা database নিয়ে কথা বলব না।

আমরা শুধু নির্ধারণ করব:

আমাদের system কোথায় শুরু?
কোথায় শেষ?
কোন external system-এর সাথে যোগাযোগ করবে?
Data flow কীভাবে চলবে?
C4 Level 1 — System Context
                           ┌─────────────────────────┐
                           │        Operator         │
                           │ (Admin / Support Team)  │
                           └─────────────┬───────────┘
                                         │
                                         ▼
                              AI Automation Platform
                                         ▲
                                         │
                           ┌─────────────┴─────────────┐
                           │                          │
                           │        Customer          │
                           │ (WhatsApp / Messenger)   │
                           └──────────────────────────┘

Platform-এর বাইরে সবাই External Actor।

External Actors
Customer

যে ব্যক্তি WhatsApp, Facebook, Instagram, Telegram, Live Chat বা অন্য কোনো channel দিয়ে যোগাযোগ করবে।

Capabilities:

Message পাঠাবে
File পাঠাবে
Voice পাঠাবে
Booking request করবে
Support চাইবে

Customer-এর platform-এর internal data-তে কোনো access থাকবে না।  


Operator

Workspace-এর member।

Examples:

Admin
Manager
Support Agent
Social Media Manager

Capabilities:

Inbox পরিচালনা
AI configure করা
Conversation assign করা
Workflow তৈরি করা
Analytics দেখা
Core System

Platform-এর responsibility:

Multi-channel communication
AI response generation
Conversation management
Memory management
Knowledge retrieval
Workflow execution
Human handoff
Reporting
External Systems
Communication Providers
WhatsApp Business API
Facebook Messenger
Instagram
Telegram
Gmail
Live Chat

Platform কখনও সরাসরি protocol নিয়ে কাজ করবে না।

সব Integration Hub-এর মাধ্যমে আসবে।

AI Providers
OpenAI
Claude
Gemini
Future Models

সব Provider Adapter Layer-এর মাধ্যমে যুক্ত হবে।

Storage
PostgreSQL
Redis
S3 / R2

Infrastructure component।

Business module এগুলো সম্পর্কে জানবে না।

Authentication
Better Auth

Future:

Auth.js
Keycloak
Custom Provider
Payment

Future:

Stripe
SSLCommerz
Lemon Squeezy
Paddle

V1-এ implement হবে না।

System Boundary

Platform-এর ভিতরে:

Identity
Workspace
Communication
Agent Runtime
Knowledge
Memory
Workflow
Integration Hub
Notification
Analytics
Administration

Platform-এর বাইরে:

Meta
OpenAI
Redis
PostgreSQL
WhatsApp
Gmail
Stripe

এগুলো Infrastructure / External Services।

High-Level Request Flow
Customer
      │
      ▼
WhatsApp
      │
      ▼
Integration Hub
      │
      ▼
Communication
      │
      ▼
Agent Runtime
      │
      ├── Memory
      ├── Knowledge
      ├── Tools
      └── LLM
      │
      ▼
Communication
      │
      ▼
Integration Hub
      │
      ▼
WhatsApp
      │
      ▼
Customer

এটাই V1-এর মূল execution path।

Human Handoff Flow
Customer
      │
      ▼
AI Agent
      │
Need Human?
      │
 ┌────┴────┐
 │         │
No        Yes
 │         │
 ▼         ▼
Reply   Operator Inbox
             │
             ▼
        Human Response
             │
             ▼
         Customer

এটি V1-এর জন্য অত্যন্ত গুরুত্বপূর্ণ feature।

System Responsibilities

Platform করবে:

Conversation orchestration
AI execution
Memory lifecycle
Knowledge retrieval
Workflow execution
Human collaboration
Audit logging

Platform করবে না:

WhatsApp protocol implement
LLM internals manage
Payment gateway logic
Social platform business logic

এসব Provider Layer-এর দায়িত্ব।

Architectural Boundary Rule

Business Module কখনও:

OpenAI SDK import করবে না।
WhatsApp SDK import করবে না।
Redis client import করবে না।
Prisma client সরাসরি expose করবে না।

সব access abstraction-এর মাধ্যমে হবে।

Non-Goals (V1)

V1-এ থাকবে না:

Multi-Agent Collaboration
Voice Agent
Video Call
Marketplace
Plugin Store
Mobile App
Visual Workflow Builder

শুধু foundation থাকবে।

Definition of Done

এই document complete হবে যখন:

System boundary স্পষ্ট।
External actor নির্ধারিত।
External system নির্ধারিত।
Request flow নির্ধারিত।
Human handoff flow নির্ধারিত।
Responsibility boundary স্পষ্ট।