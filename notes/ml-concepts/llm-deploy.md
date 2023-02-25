---
date: 2/24/23 
---

# Technical details behind deploying LLM's 

Will be an ongoing thread of cool ideas I come across. 


- Using [fly.io](https://fly.io/) to distribute inference in a geographically optimized fashion.
- Having multiple backends for chatbots/LLM's (i.e. openai --> cohere pipeline) if one fails/server is down/request doesn't work. 
- [Supabase and vector embeddings](https://supabase.com/blog/openai-embeddings-postgres-vector)