# GenAI Interview Prep

## Pros and cons of AI

### Pros
- **Speed**: automates repetitive work (boilerplate, test scaffolding, docs, data extraction) so engineers spend time on design and hard problems.
- **Handles unstructured data**: can pull structure out of messy text (resumes, transcripts, support tickets) where rule-based code breaks down.
- **Faster debugging and learning**: good at suggesting hypotheses and explaining unfamiliar code or libraries.
- **Natural-language interfaces**: lets users ask questions instead of navigating menus (e.g., asking a video a question in Verbatim).

### Cons
- **Hallucination**: produces confident, wrong answers. Outputs need grounding (retrieval, citations) and verification.
- **Non-determinism**: the same input can give different outputs, which makes testing and consistent scoring harder.
- **Cost and latency**: every call costs money and adds response time, and both grow with token count and scale.
- **Data privacy and security**: sending user data to a third-party API, plus risks like prompt injection.
- **Over-reliance**: engineers can accept output they don't understand. You still own the code you ship.

### My own experience
- **Pro**: on the Verbatim chunking bug, AI-assisted debugging helped me narrow down hypotheses faster.
- **Con**: I still had to decide what to log, read the output, and confirm the root cause myself. I verified the fix against about 30 questions with known answers and timestamps, not against the AI's word.
- **Con in production**: Resume Analyzer's LLM scoring can be inconsistent depending on prompt behavior, and embedding similarity can overestimate relevance. That's why I paired the LLM with a fixed weighted rubric instead of trusting a single AI score.

## Optimizing token usage for a chatbot

### Input tokens (usually the biggest cost)
- **Retrieve, don't stuff**: send only the most relevant chunks instead of whole documents. Verbatim sends the top 5 chunks, not the full transcript.
- **Manage conversation history**: keep the last N turns, and summarize older turns into a short running summary instead of resending the full history every call.
- **Tighten the system prompt**: remove redundant instructions and examples; it's re-sent on every request.
- **Prompt caching**: keep the static parts of the prompt (system prompt, instructions) at the start and identical across calls so the provider can reuse cached prefixes.
- **Chunk size tuning**: smaller, well-bounded chunks mean less irrelevant text per retrieval.

### Output tokens
- **Cap max output tokens** for each use case.
- **Ask for concise or structured output**: JSON with specific fields instead of open-ended prose (Resume Analyzer uses JSON mode).

### Model choice
- **Model tiering**: use a small, cheap model by default and escalate to a larger one only where quality matters. Resume Analyzer uses gpt-4.1-mini for extraction, matching, and interview questions, and gpt-4.1 only for bullet rewrites.
- **Route simple requests away from the LLM entirely**: FAQs, greetings, or known intents can be answered from cache or rules.

### Avoid repeat work
- **Cache responses** for identical or near-identical questions.
- **Cache embeddings**: embed a document once at ingestion and store it (pgvector), never re-embed it per query.

### Measure it
- **Track tokens and cost per request**: Resume Analyzer's full upload, analysis, and match flow costs under $0.001; the most expensive single call is a bullet rewrite at about $0.003.

## My projects as examples
- **Verbatim (RAG)**: transcripts chunked into ~500 words with ~50-word overlap, embedded with text-embedding-3-small, stored in pgvector, top 5 chunks sent to GPT-4o with timestamps. The system prompt asks the model to cite timestamps and say when it's inferring rather than quoting.
- **Resume Analyzer (not RAG)**: the full resume and job description go to the model; embeddings are used only for cosine similarity scoring. Model tiering and JSON mode keep cost and parsing predictable.

## Likely follow-ups
- RAG vs. fine-tuning: when would you use each?
- How do you reduce hallucinations? (Grounding with retrieval, citations, telling the model to say when it doesn't know, verifying against known answers.)
- How would you evaluate a chatbot's quality? (A test set of questions with expected answers, like my 30-question doc for Verbatim.)