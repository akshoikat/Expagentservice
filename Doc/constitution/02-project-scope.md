Document 02

docs/constitution/02-project-scope.md

1. Platform Scope

এই platform-এর মূল উদ্দেশ্য হলো AI-driven business communication, automation এবং agent execution।

Platform-এর responsibility:

Identity & Organization
Authentication
Authorization
Workspaces
Teams
Roles
Permissions
Communication Hub

Supported Channels (architecture level)

WhatsApp
Facebook Messenger
Instagram
Telegram
Gmail
Live Chat
Webhook
Future Connectors
AI Runtime
Agent Execution
Persona
Prompt Management
Tool Calling
Planning
Context Assembly
Multi-Provider LLM Support
Memory System
Short-term Memory
Long-term Memory
Semantic Memory
User Memory
Conversation Memory
Knowledge System
Documents
FAQ
Website Crawl
PDF
Google Docs
API Data
Vector Search
Workflow Engine
Trigger
Condition
Delay
Loop
Parallel Execution
Human Approval
Retry
Scheduling
Integration Platform
CRM
Calendar
Payment
Email
SMS
REST API
Webhooks
Analytics
Usage
Token Cost
Conversation Metrics
Agent Performance
Workflow Performance
Business KPIs
Administration
Workspace Management
Billing
Subscription
API Keys
Audit Logs
System Settings
2. Out of Scope

এই platform-এর core responsibility নয়:

ERP
Accounting
CMS
E-commerce Storefront
Video Conferencing
Office Suite
IDE
Social Network

প্রয়োজনে এগুলোর সাথে integration হবে, কিন্তু এগুলো platform-এর অংশ হবে না।

3. First Product (V1)

V1-এ আমরা একটি usable product deliver করব।

Product Name (Working):

Social Media AI Automation

V1-এর objective:

Workspace তৈরি
User Login
WhatsApp Cloud API
Unified Inbox
Manual Reply
Contact Management
Conversation History
AI Reply Suggestion
AI Auto Reply (configurable)
Basic Knowledge Base
Basic Memory
Agent Configuration
Audit Log

এখানে workflow builder, visual editor, marketplace, multi-agent orchestration—এসব পরে আসবে।

4. Future Products

একই platform-এর উপর ভবিষ্যতে:

Hotel Reception AI
Medical Reception AI
CRM AI Assistant
HR Assistant
Sales Assistant
Appointment Booking Agent
E-commerce Assistant
Internal Company Assistant

সবগুলো module হিসেবে তৈরি করা যাবে।

system-এর backbone।

┌─────────────────────────────────────────────┐
│ Presentation Layer                          │
│ Web Dashboard • Admin • Inbox • API Clients │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│ Application Layer                           │
│ Use Cases • Services • Commands • Queries   │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│ AI Runtime Layer                            │
│ Agents • Memory • Knowledge • Prompt Engine │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│ Automation Layer                            │
│ Workflow • Events • Queue • Scheduler       │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│ Integration Layer                           │
│ WhatsApp • Meta • Gmail • Telegram • APIs   │
└─────────────────────────────────────────────┘
                    │
┌─────────────────────────────────────────────┐
│ Infrastructure Layer                        │
│ PostgreSQL • Redis • Vector DB • Storage    │
└─────────────────────────────────────────────┘

আমি এই architecture-টা এখনই define করতে চাই, কারণ এরপরের প্রতিটি document (Technology Stack, Domain Model, Database, API, Folder Structure) এই layer অনুযায়ী তৈরি হবে।

