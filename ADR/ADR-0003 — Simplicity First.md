আমাদের design principle হবে:

Enterprise Architecture, Startup Complexity.

অর্থাৎ architecture future-proof হবে, কিন্তু implementation যতটা সম্ভব সহজ থাকবে।

এর জন্য আমি কিছু নিয়ম এখনই lock করতে চাই।

🔒 ADR-0003 — Simplicity First

আমাদের project-এর প্রতিটি decision এই rule follow করবে।

Rule 1

Build only what the current version needs.

যদি V1-এ কোনো feature না লাগে, তাহলে তার code লিখব না।

আমরা শুধু extension point রেখে দেব।

উদাহরণ:

Integration Interface
        │
        ├── WhatsApp ✅
        ├── Facebook ❌ (Later)
        ├── Telegram ❌ (Later)
        └── Gmail ❌ (Later)

Facebook-এর architecture থাকবে, কিন্তু implementation থাকবে না।

Rule 2

One implementation until proven otherwise.

উদাহরণ:

LLM Provider

LLM Provider Interface
        │
        └── OpenAI Adapter

Claude, Gemini, Ollama-এর support interface level-এ ভাবা হবে, কিন্তু V1-এ শুধু OpenAI implement হবে।

Rule 3

Avoid abstraction without a real use case.

যদি abstraction-এর কোনো immediate benefit না থাকে, তাহলে সেটা এখন করব না।

Rule 4

Every module must earn its existence.

নতুন module যোগ করার আগে প্রশ্ন হবে:

এর আলাদা lifecycle আছে?
আলাদা responsibility আছে?
ভবিষ্যতে আলাদা maintain করতে হবে?

যদি উত্তর "না" হয়, তাহলে নতুন module হবে না।

Rule 5

Optimize for readability, not cleverness.

এক বছর পরে code খুলে যেন ১০ মিনিটে বোঝা যায়।