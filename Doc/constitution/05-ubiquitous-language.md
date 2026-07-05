Document 05

docs/constitution/05-ubiquitous-language.md

Purpose

Platform-এর প্রতিটি শব্দের একটিই অর্থ থাকবে।

Database, API, Code, UI, Documentation—সব জায়গায় একই terminology ব্যবহার করা হবে।

একটি concept-এর জন্য একাধিক নাম ব্যবহার করা যাবে না।

Core Business Terms
Platform

সম্পূর্ণ AI Automation System.

একটি মাত্র Platform থাকবে।

Workspace

একটি Business Entity বা Tenant।

উদাহরণ

ABC Hotel

XYZ Hospital

My Agency

Tech Company

প্রতিটি Workspace সম্পূর্ণ isolated।

User

Platform ব্যবহারকারী মানুষ।

Examples

Admin
Manager
Operator
Support Agent

AI কখনও User হবে না।

Contact

যে ব্যক্তি Workspace-এর সাথে যোগাযোগ করছে।

Examples

Customer
Guest
Client
Patient
Lead

Contact কখনও User নয়।

Channel

Communication Medium.

Examples

WhatsApp
Facebook Messenger
Instagram DM
Telegram
Gmail
Live Chat

নিয়ম:

Conversation সবসময় একটি Channel-এর মাধ্যমে শুরু হবে।

Conversation

Contact এবং Workspace-এর মধ্যে একটি চলমান যোগাযোগ।

Conversation-এর মধ্যে অনেক Message থাকবে।

Message

Conversation-এর একটি atomic communication unit।

Examples

Text
Image
Audio
Document
Location
Template
Inbox

Workspace-এর Conversation List.

Inbox data store নয়।

Inbox একটি View।

Agent

AI Worker.

Agent একটি role execute করে।

Examples

Customer Support Agent
Social Media Agent
Booking Agent
HR Agent
Persona

Agent-এর আচরণ।

Persona define করবে

Tone
Style
Personality
Restrictions
Tool

Agent যে capability invoke করতে পারে।

Examples

CRM
Calendar
WhatsApp API
Email
Google Maps
Workflow

একটি automation process।

Workflow

Trigger

↓

Conditions

↓

Actions

↓

Completed

Trigger

Workflow শুরু করার event।

Examples

Message Received
Booking Created
Human Assigned
Action

Workflow-এর একটি executable step।

Examples

Send Message
Update CRM
Create Calendar Event
Memory

Agent-এর learned context.

Memory দুই ধরনের:

Short-term
Long-term

Memory user-specific হতে পারে।

Knowledge

Business information.

Examples

FAQ
PDF
Website
Pricing
Policies

Knowledge static।

Memory dynamic।

Integration

External System Connector.

Examples

WhatsApp
Stripe
Google Calendar
Shopify
Provider

Integration-এর implementation.

উদাহরণ

LLM Provider

    OpenAI

    Claude

    Gemini

Event

Platform-এর ভিতরে ঘটে যাওয়া গুরুত্বপূর্ণ ঘটনা।

Examples

Conversation Created
Message Received
Agent Assigned
Task

Background execution।

Examples

Retry
Sync
Import
Export
Job

Queue-তে থাকা executable task।

BullMQ / Temporal-এর execution unit।

Execution

Workflow-এর একটি runtime instance।

Workflow template আর Execution এক জিনিস নয়।

Audit Log

Security history।

কে কী করেছে তার immutable record।

Forbidden Terms

নিচের শব্দগুলো project-এ ব্যবহার করব না, কারণ এগুলোর অর্থ অস্পষ্ট বা duplicate।
Bot

Chat Bot

AI Bot

Thread

Chat

Customer Chat

FB User

WA User

Messenger User

Prompt Template (অস্পষ্ট)

এসবের পরিবর্তে নির্দিষ্ট শব্দ ব্যবহার করব:

Agent
Conversation
Contact
Prompt

Naming Rules

একটি concept-এর জন্য একটি নাম।

উদাহরণ:
❌ Chat

❌ Thread

❌ Session

✅ Conversation
❌ Customer

❌ Client

❌ Guest

❌ Patient

✅ Contact
Business layer-এ সবাই Contact।
❌ AI

❌ Bot

❌ Assistant

✅ Agent
❌ Company

❌ Organization

❌ Tenant

✅ Workspace

Semantic Hierarchy
Platform
    │
    ▼
Workspace
    │
    ▼
Channel
    │
    ▼
Conversation
    │
    ▼
Message

Agent
    │
    ├── Persona
    ├── Memory
    ├── Knowledge
    └── Tools
Workflow
    │
    ├── Trigger
    ├── Condition
    ├── Action
    └── Execution

    🔒 ADR-0004 — Controlled Vocabulary

Decision: The platform will use a single, controlled vocabulary across code, APIs, database schema, UI, documentation, and tests.

Reason:

Eliminates ambiguity.
Reduces naming drift.
Makes onboarding easier.
Simplifies searching the codebase.
Improves long-term maintainability.

