<p align="center">
  <img src="https://wauldo.com/favicon.svg" alt="Wauldo" width="120" />
</p>

<h1 align="center">Wauldo</h1>

<p align="center">
  <strong>Verified AI answers from your documents — grounded, or refused.</strong>
</p>

<p align="center">
  <a href="https://wauldo.com/demo">Demo</a> &bull;
  <a href="https://wauldo.com/docs">Docs</a> &bull;
  <a href="https://rapidapi.com/binnewzzin/api/smart-rag-api">RapidAPI</a> &bull;
  <a href="https://wauldo.com/leaderboard">Benchmarks</a>
</p>

---

Wauldo is an API for **verified AI agents**: every answer is checked against its sources and comes with a support score from 0 to 1.

Build your own agents through the API, or upload documents and ask questions: you get answers grounded in your sources — or no answer if it cannot be verified.

## Verification by Design

Most RAG systems retrieve context and assume the model gets it right.
Wauldo verifies the answer before returning it.

Benchmark results, methodology and the MIT-licensed bench are on the [public leaderboard](https://wauldo.com/leaderboard).

## Request Flow

```
Upload document (PDF, DOCX, images, text)
        |
   Ask a question
        |
   Retrieve relevant chunks (BM25 + vector hybrid)
        |
   Extract key facts from sources
        |
   Generate answer (LLM)
        |
   Verify grounding against sources
        |
   +-- Verified? --> Return answer + citations
   +-- Not verified? --> Return "insufficient evidence"
```

## Key Features

Wauldo introduces a verification layer on top of standard RAG pipelines:

- **Pre-generation fact extraction** — key values injected as constraints before the LLM call
- **Post-generation grounding check** — every answer verified against sources
- **Citation validation** — detects phantom references
- **Verified agents** — custom agents through the API, every run's answer checked and scored
- **Fact-check API** — verify any LLM output against any source
- **Quality scoring** — document upload includes extraction quality metrics
- **OpenAI-compatible** — drop-in replacement for existing integrations

## SDKs

| Language | Package | Install | Repo |
|----------|---------|---------|------|
| Python | [wauldo](https://pypi.org/project/wauldo/) | `pip install wauldo` | [wauldo-sdk-python](https://github.com/wauldoai/wauldo-sdk-python) |
| JavaScript | [wauldo](https://www.npmjs.com/package/wauldo) | `npm install wauldo` | [wauldo-sdk-js](https://github.com/wauldoai/wauldo-sdk-js) |
| Rust | [wauldo](https://crates.io/crates/wauldo) | `cargo add wauldo` | [wauldo-sdk-rust](https://github.com/wauldoai/wauldo-sdk-rust) |

```python
from wauldo import HttpClient

# Free key from RapidAPI (see the links above): use the RapidAPI host.
client = HttpClient(
    base_url="https://smart-rag-api.p.rapidapi.com",
    headers={
        "X-RapidAPI-Key": "YOUR_RAPIDAPI_KEY",
        "X-RapidAPI-Host": "smart-rag-api.p.rapidapi.com",
    },
)
# Enterprise key: HttpClient(base_url="https://api.wauldo.com", api_key="YOUR_API_KEY")

client.rag_upload(content="Refunds are accepted within 30 days of purchase.", filename="policy.txt")
result = client.rag_query("What is the refund policy?")

print(result.answer)
print("Grounded in your sources:", result.get_grounded())
print("Confidence:", result.get_confidence())
```

## Built For

- Production RAG systems requiring factual reliability
- Internal knowledge bases and customer support automation
- Regulated domains (legal, insurance, healthcare, compliance)
- Applications where "confidently wrong" is worse than "I don't know"

## Architecture

Built in Rust. Hybrid retrieval. No vendor lock-in.

Model-agnostic pipeline: performance is driven by verification rather than model size.

---

<p align="center">
  <a href="https://wauldo.com">Website</a> &bull;
  <a href="https://wauldo.com/demo">Try the Demo</a> &bull;
  <a href="https://wauldo.com/docs">API Docs</a> &bull;
  <a href="https://rapidapi.com/binnewzzin/api/smart-rag-api">Free Tier</a>
</p>
