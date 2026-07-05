🔒 PDS Rule-001
Technology is Replaceable

আমরা কখনো code-কে technology-এর সাথে bind করব না।

উদাহরণ:

❌ Wrong

ConversationService

↓

OpenAI SDK

এতে পরে OpenAI পরিবর্তন করা কঠিন হবে।

✅ Correct

ConversationService

↓

LLM Interface

↓

OpenAI Adapter

এখন Claude, Gemini, Ollama যোগ করতে ConversationService পরিবর্তন লাগবে না।

এই rule শুধু AI না, সবকিছুর জন্য প্রযোজ্য।