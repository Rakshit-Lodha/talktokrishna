# Talk to Krishna

An AI-powered spiritual counselor providing guidance from the Bhagavad Gita for modern life problems, especially heartbreak and emotional healing.

**Status: Working MVP, 60-70% accuracy**

---

## What It Does

**You ask:** "My girlfriend left me"

**Krishna responds:**
> Hey Vats, I understand that you're going through a tough time with your girlfriend leaving you. Heartbreak can be incredibly painful, but remember that you are not alone in this journey.
> 
> Reflect on this verse: "Always think of Me, become My devotee, worship Me and offer your homage unto Me. Thus you will come to Me without fail." In moments of sorrow, turning your thoughts towards a higher purpose or spiritual connection can bring you comfort and clarity.
> 
> It's okay to feel sadness, but trust that with time and devotion to your own well-being, you will find your way to happiness again.

---

## Architecture

### Two-Stage RAG System
```
User Query
    ↓
Stage 1: Semantic Search (Embeddings)
    ├─ OpenAI text-embedding-3-small
    ├─ ChromaDB vector database
    └─ Returns top 10 relevant verses
    ↓
Stage 2: LLM Re-Ranking
    ├─ GPT-4o-mini filters 10 → 1-3 best verses
    ├─ Selects most relevant to user's pain
    └─ Generates empathetic response
    ↓
Krishna's Response
    ├─ Personalized opening
    ├─ Verse citations
    └─ Hopeful conclusion
```

### Why Two Stages?

**Embeddings alone:** ~60-70% relevance
**+ LLM re-ranking:** ~75-85% relevance

Fast retrieval + intelligent selection = better responses

---

## Performance

### Current Metrics (v1.0)
- **Accuracy:** 60-70% (verse relevance to query)
- **Response Time:** ~3-4 seconds
- **Database:** Krishna's direct teachings only (filtered from 700 verses)
- **Model:** GPT-4o-mini for re-ranking + content generation

---

## Tech Stack

**Vector Database:**
- ChromaDB for embedding storage
- Persistent local collection

**Embeddings:**
- OpenAI `text-embedding-3-small`
- 1536 dimensions
- Cosine similarity search

**LLM:**
- GPT-4o-mini for re-ranking
- Temperature: 0.7
- Custom system prompts

**Data:**
- Bhagavad Gita (Prabhupada translation)
- Filtered to Krishna's verses only
- 520 verses (from original 700)


---

## How It Works

### 1. Data Preparation
```python
# Filter to Krishna's direct teachings
krishna_verses = [
    v for v in all_verses 
    if is_krishna_speaking(v) and is_practical_wisdom(v)
]
```

### 2. Embedding Creation
```python
# Batch embed all verses
embeddings = create_embeddings_batch(
    texts=krishna_verses,
    batch_size=100
)
```

### 3. Query Processing
```python
def query(user_input):
    # Stage 1: Retrieve top 10
    results = collection.query(
        query_embeddings=[get_embedding(user_input)],
        n_results=10
    )
    
    # Stage 2: LLM picks best 1-3
    response = gpt_rerank_and_respond(
        query=user_input,
        verses=results['documents'][0]
    )
    
    return response
```

---

## 💻 Installation
```bash
# Clone repo
git clone https://github.com/yourusername/talktokrishna.git
cd talktokrishna

# Install dependencies
pip install openai chromadb python-dotenv

# Set up environment
cp .env.example .env
# Add your OPENAI_API_KEY to .env

# Run
python main.py
```
---
