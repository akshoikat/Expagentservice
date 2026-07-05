Document 04

docs/constitution/04-core-domain-model.md

Principle

Platform feature দিয়ে নয়, business domain দিয়ে তৈরি হবে।

Core Domain Map
AI Automation Platform
│
├── Identity
│
├── Workspace
│
├── Communication
│
├── Agent Runtime
│
├── Knowledge
│
├── Memory
│
├── Workflow
│
├── Integration Hub
│
├── Notification
│
├── Analytics
│
├── Billing
│
└── Administration

এখন প্রতিটি Domain-এর দায়িত্ব নির্ধারণ করি।

1. Identity

Purpose

User কে authenticate এবং authorize করা।

Contains:

User
Role
Permission
Session
API Key

এটা কখনও Conversation বা Agent-এর business logic জানবে না।

2. Workspace

একটি organization-এর boundary।

Contains:

Organization
Workspace
Team
Members
Settings

Workspace হলো tenant boundary।

3. Communication

এটাই V1-এর সবচেয়ে গুরুত্বপূর্ণ domain।

Contains:

Contact
Conversation
Message
Inbox
Assignment
Labels

WhatsApp, Facebook, Telegram—সব message এখানে unified হবে।

4. Agent Runtime

AI execution।

Contains:

Agent
Persona
Prompt
Tool Registry
Model
AI Session

Business-specific knowledge এখানে থাকবে না।

5. Knowledge

Contains:

Documents
FAQ
Web Pages
PDFs
Embeddings
Retrieval
6. Memory

Contains:

User Memory
Conversation Memory
Long-term Memory
Semantic Memory

Knowledge আর Memory আলাদা domain থাকবে। এটা ভবিষ্যতে অনেক সুবিধা দেবে।

7. Workflow

Contains:

Workflow
Trigger
Action
Condition
Execution
Scheduler
8. Integration Hub

Contains:

WhatsApp
Meta
Telegram
Gmail
Webhooks

সব provider adapter pattern follow করবে।

9. Notification

Contains:

Email
Push
SMS
Internal Notification
10. Analytics

Contains:

Usage
Reports
Metrics
Token Usage
Agent Performance
11. Billing

Contains:

Subscription
Invoice
Usage
Payment

V1-এ minimal থাকবে।

12. Administration

Contains:

Audit Logs
System Config
Feature Flags
Platform Settings


Domain Relationships

Workspace
│
├── Identity
├── Communication
├── Agent Runtime
├── Knowledge
├── Workflow
└── Analytics

Communication
│
├── Agent Runtime
├── Memory
├── Knowledge
└── Integration Hub

Workflow
│
├── Agent Runtime
├── Communication
├── Notification
└── Integration Hub

একটি গুরুত্বপূর্ণ refinement

আমি Communication domain-এর মধ্যে "Channel" entity যোগ করার প্রস্তাব দিচ্ছি।

এখন পর্যন্ত আমরা WhatsApp, Facebook, Instagram আলাদা integration হিসেবে দেখছিলাম। কিন্তু business level-এ এগুলো আসলে Channel।

তাই model হবে:

Channel
│
├── WhatsApp
├── Facebook Messenger
├── Instagram DM
├── Telegram
├── Gmail
└── Live Chat

তারপর
Channel
    │
    ▼
Conversation
    │
    ▼
Messages

