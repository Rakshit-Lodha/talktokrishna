# Complete RAG System - talktokrishna Foundation

## What It Does

AI spiritual counselor using Bhagavad Gita teachings for heartbreak and life guidance.

**Example:**

**User:** "My gf left me"

**Krishna:** "Hey Vats, I understand that you're going through a difficult time right now. 
It's important to remember that the mind can be your friend or your enemy. Focus on your own growth and well-being. 
You have the right to work only, but never to its fruits, meaning you should focus on your actions and duties without being attached to the outcomes. 
Be steadfast in yoga and perform your duty, as consistent effort and self-care will guide you through this challenging period."

## Architecture
```
User Query
    ↓
OpenAI Embeddings
    ↓
ChromaDB Semantic Search (3 verses)
    ↓
GPT-3.5-turbo Generation
    ↓
Empathetic Krishna Response
```

## Key Features

1. **Semantic Understanding**
   - "My gf left me" → Finds mind control + detachment verses
   - Not keyword matching
   - Emotional intelligence

2. **Grounded Responses**
   - Only uses provided context
   - Admits when doesn't know
   - No hallucination

## Tech Stack

- ChromaDB for vector storage
- OpenAI embeddings (text-embedding-3-small)
- GPT-4o for generation
- Python
