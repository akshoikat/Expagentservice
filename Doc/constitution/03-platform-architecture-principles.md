Constitution Document 03

docs/constitution/03-platform-architecture-principles.md

Platform Architecture Philosophy

আমাদের architecture পাঁচটি মূল নীতির উপর দাঁড়াবে।

1. Modular Monolith First

এটাই প্রথম বড় architectural decision।

আমরা Microservices দিয়ে শুরু করব না।

আমরা Modular Monolith দিয়ে শুরু করব।

কারণ

আমাদের V1-এ

Authentication
Workspace
AI
Inbox
Workflow
WhatsApp
Knowledge

সবই tightly related।

2. Domain Driven Modules

আমরা feature অনুযায়ী folder বানাব না।

আমরা domain অনুযায়ী module বানাব।

উদাহরণ:

❌ Wrong

controllers/

services/

models/

utils/

----------------------

✅ Correct

identity/

workspace/

conversation/

agent/

knowledge/

workflow/

analytics/

3. Vertical Slice Architecture

একটি feature-এর সবকিছু এক জায়গায় থাকবে।

উদাহরণ:

conversation/

    api/

    application/

    domain/

    infrastructure/

    tests/

অন্য folder-এ conversation-এর code থাকবে না।
4. Dependency Rule

সবচেয়ে গুরুত্বপূর্ণ rule।

Dependency সবসময় নিচের দিকে যাবে।
UI

↓

Application

↓

Domain

↓

Infrastructure

Infrastructure কখনও Domain-কে control করবে না।

Domain কখনও React, Prisma, PostgreSQL, Redis, OpenAI SDK সম্পর্কে জানবে না।

5. Everything is a Module

Platform-এর প্রতিটি capability একটি module।

যেমন
Identity

Workspace

Conversation

Inbox

Contact

Agent

Knowledge

Memory

Workflow

Integration

Notification

Analytics

Billing

Audit

প্রতিটি module-এর নিজস্ব:

API
Database access
Events
Tests
Documentation

থাকবে।

এরপর Architecture Views

এখানেই আমি একটু ভিন্নভাবে এগোতে চাই।

আমি চাই আমরা শুরু থেকেই C4 Model অনুসরণ করি।

এটা Simon Brown-এর architecture model, যা enterprise project-এ খুব ব্যবহৃত।

আমাদের ৪টি diagram থাকবে

Level 1
System Context
User

↓

AI Automation Platform

↓

WhatsApp

Facebook

Instagram

CRM

OpenAI

Payment

Calendar

Level 2
Container Diagram
Web Dashboard

↓

API Server

↓

AI Runtime

↓

Worker

↓

Database

↓

Redis

↓

Vector DB
Level 3
Component Diagram

উদাহরণ

Conversation Module
API

↓

Service

↓

Repository

↓

Database

Level 4
Code Diagram

Class

Interface

Dependency

এটা পরে আসবে।

Platform Backbone-এ

আমি project-কে ১২টি Core Domain-এ ভাগ করতে চাই।

Platform

│

├── Identity

├── Workspace

├── Communication

├── Agent Runtime

├── Knowledge

├── Memory

├── Workflow

├── Integration Hub

├── Notification

├── Analytics

├── Billing

└── Administration

এগুলো Core Domains।

