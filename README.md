# NoteGenius_LinkedIn_Post.md

---

# 🧠 I built ChatGPT — but for *your own* documents.

No API key. No data leaving your machine. No hallucinations.

Just your PDFs, a free Kaggle GPU, and an open-source LLM that only speaks from *your* knowledge base.

Let me show you what I built — and why it matters beyond the demo.

---

## The problem I was actually trying to solve

I had 44 PDFs. Hundreds of pages of study material, technical references, and research notes.

Every time I needed something, I was ctrl+F-ing, scrolling, re-reading.

So I built the thing I wish had existed.

**NoteGenius** — ask any question. Get a grounded answer. With the exact source and page number it came from.

---

## How it works under the hood

```
44 PDFs  →  20,986 contextual chunks
              ↓
         TF-IDF index  (no vector DB needed)
              ↓
    query  →  cosine similarity  →  top-3 chunks
              ↓
    Mistral-7B-Instruct  (4-bit, free T4 GPU)
              ↓
    grounded answer  +  source citation
```

The chunking overlap (200 chars) matters more than people think. Without it you get hard cuts mid-sentence and retrieval quality tanks.

I went with TF-IDF over embeddings deliberately — it's fast, has zero GPU requirements, and for keyword-heavy technical material it performs surprisingly well.

---

## But here's where it gets more interesting

Using the contextual chunks the system already generated, I created **instruction-style training pairs**:

> question → grounded answer → source

Then fine-tuned an open-source LLM directly on that domain data.

The result is a model that doesn't just *retrieve* from your documents — it starts to *think* in your domain's language.

This is the architecture behind most serious enterprise AI systems, just made visible.

```
Raw documents
     ↓
Contextual data layer
     ↓
Instruction data generation
     ↓
Domain fine-tuned model
     ↓
Intelligent assistant
```

---

## Real numbers: Open-source vs Paid API

I built a live cost comparison into the app. Here's what a typical request actually looks like:

**Token usage**
- Input: 1,240 tokens
- Output: 220 tokens
- Total: 1,460 tokens

**Cost per request**

| Model | Cost |
|---|---|
| GPT-4o mini | ~$0.000318 |
| GPT-4.1 | ~$0.004240 |
| GPT-5.4 | ~$0.006400 |
| Self-hosted (estimated) | ~$0.000270 |

*Assumptions: $8/hr GPU, 120 tokens/sec throughput*

At small scale, API wins on simplicity.

At large scale and for private data, open-source wins on cost, control, and customisation.

The real decision isn't cost per request — it's **architecture strategy**.

---

## Where this actually goes at enterprise scale

The same pattern scales directly into production systems across industries:

**🏥 Healthcare**
Clinical knowledge assistants · Medical documentation support · Report summarisation

**💰 Finance**
Financial report analysis · Compliance Q&A · Regulatory knowledge retrieval

**🏢 Enterprise**
Internal documentation assistants · Policy Q&A · Contextual insights from private data

The underlying architecture is identical. The domain data is what changes.

---

## Who I built this for

I built **NoteGenius** specifically for learners in this community.

Students, working professionals, anyone drowning in PDFs during a learning sprint.

Instead of scrolling — just ask. The answer comes back with the source, grounded in your own material. No guessing. No hallucination.

Small experiments like this reveal the skeleton of much larger systems.

---

## Try it yourself

🔗 **Live app** (active ~1 week): https://fdf5f309024ac86b60.gradio.live

💻 **Full code**: https://github.com/venkatak07-cmd/NoteGenius.git

Point it at your own PDFs and see what happens.

---

I'd genuinely love feedback from this community on:

→ retrieval quality on your own documents
→ where grounded responses break down
→ use cases I haven't thought of yet

If there's enough interest I'll open-source the full fine-tuning pipeline and host a permanent version.

Drop a comment or DM — happy to share the notebook.

---

*#NoteGenius #RAG #LLM #FineTuning #Mistral #OpenSourceAI #MachineLearning #GenerativeAI #AIEngineering #BuildInPublic #EnterpriseAI #Kaggle*
