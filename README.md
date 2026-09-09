<img src="https://github.com/user-attachments/assets/9a8e3477-0475-4a96-82cb-b010d54741f9" alt="Muhammad Abdullah — AI Developer, Python Innovator, Multi-Agent Specialist" />

# Muhammad Abdullah

**Applied ML and full-stack engineering — models, the services that serve them, and the interfaces people actually use.**

Final-year Mechatronics student (8th semester) in Hyderabad, Pakistan. I build systems end to end: train the model, wrap it in an API that fails gracefully, and put a real interface in front of it. The part I care most about is what happens when the model is wrong, the network is gone, or the data is thinner than the claim.

---

## Saans — paediatric TB screening for community health workers

An offline-first tablet app that implements the WHO *Operational Handbook on Tuberculosis, Module 5* (2022) treatment decision algorithm, with three ML assists that inform the health worker but are structurally prevented from changing the score.

**[→ ra189zor/Saans](https://github.com/ra189zor/Saans)** · React 19 · Vite · Tailwind 4 · FastAPI · TensorFlow · scikit-learn · onnxruntime · Docker

| Component | What it does | Measured |
| --- | --- | --- |
| **Chest X-ray model** | DenseNet121 fine-tuned on 13,265 films from four public sources, deduplicated by perceptual hash before splitting. Returns a probability plus a Grad-CAM heatmap. | 95.1% recall, 98.2% specificity on 1,990 held-out films. **AUC 0.942** |
| **Cough analysis** | RandomForest over 66 acoustic features — MFCCs with deltas, zero-crossing rate, spectral centroid and rolloff, burst statistics. | AUC 0.951 on under-fives, evaluated by age band rather than assumed |
| **WHO handbook assistant** | Two-stage local retrieval over 1,055 passages: MiniLM bi-encoder on onnxruntime, then a cross-encoder rerank. Answers cite a page or refuse. | ~3 ms retrieval; refusal guard fires before any API call |

Three things about this project matter more than the numbers:

**The reported AUC is 0.942, not the 0.995 the pooled test set produces.** One source contributes TB and normal films from different collections that differ for reasons unrelated to disease, so the model separates them without reading pathology. The honest benchmark is the single hospital where both classes share equipment. Quoting the inflated figure would have been easy and wrong.

**The model never decides.** Every finding is confirmed by the health worker before it reaches the scorer, and removing the X-ray model entirely leaves a working app — WHO's Algorithm B is designed for clinics without an X-ray at all. The cough result is a hint that is never passed to the scorer, because WHO scores cough by *duration* and ten seconds of audio cannot measure two weeks.

**Every model here was trained on adults**, because no public paediatric TB X-ray or cough dataset exists. Rather than train on a mixture and hope, every recording from anyone under 18 was held out and the adult-trained model was then scored by age group. The [Limitations](https://github.com/ra189zor/Saans#limitations) section documents what that costs.

Bilingual English/Urdu with full RTL layout, installable as a PWA and fully functional offline, ten illustrated clinical guides built through a WebP pipeline that cuts 16.7 MB to 693 KB, and an opt-in field data collection path with per-capture consent and no identifying fields written to disk.

---

## Selected work

| Project | What it is | Stack |
| --- | --- | --- |
| **[llm-observe-hub](https://github.com/ra189zor/llm-observe-hub)** | An OpenAI-compatible proxy that sits in front of local LLMs and instruments them — streaming pass-through, per-request cost and latency logging, a configurable alert rule engine, budget tracking and model comparison. Observability as a sidecar, not a library you have to import. | FastAPI, SQLAlchemy, httpx, Chart.js |
| **[WorkflowWizard](https://github.com/ra189zor/WorkflowWizard)** | Turns a plain-English automation description into importable n8n workflow JSON, validated before export. Built as a product rather than a demo: session auth, Postgres persistence, subscription billing and usage metering. | React, TypeScript, Express, Drizzle ORM, Neon Postgres, Passport, Paddle |
| **[fraud-detection-agent](https://github.com/ra189zor/fraud-detection-agent)** | Hybrid transaction scoring — an unsupervised detector (Isolation Forest / One-Class SVM) running alongside a six-signal rule engine covering amount, merchant risk, geography, velocity, timing and device. Analyst feedback is captured and retrains the model; an LLM turns each flag into a readable explanation. | Python, scikit-learn, Streamlit, SQLite |
| **[MCP-Studio](https://github.com/ra189zor/MCP-Studio)** | Generates and validates MCP server implementations from a description, fanning the same task out to Anthropic, OpenAI and Google models in parallel and reconciling their output. Includes a code validator and an in-app test harness. | Python, Streamlit, asyncio, PostgreSQL |
| **[AI-Venture-Capital-Scout](https://github.com/ra189zor/AI-Venture-Capital-Scout)** | Startup screening that pairs a CrewAI agent crew with a TensorFlow founder-success model trained separately in a notebook, plus document ingestion and a market saturation score. | CrewAI, LangChain, TensorFlow, scikit-learn |

**[MindFlow](https://github.com/ra189zor/MindFlow)** and **[JobNexus](https://github.com/ra189zor/JobNexus)** are where the multi-agent pattern I keep reaching for got worked out: specialist agents behind a validator agent that checks their output against the original constraints and sends it back for revision until it passes or hits a revision cap. MindFlow applies it to a five-stage research-and-writing pipeline with retries, concurrency throttling and response caching; JobNexus to skill-gap analysis, with fuzzy matching and a synonym dictionary so a user is never penalised for how they spelled a technology.

---

## How I build

The projects above have more in common than their stacks suggest.

**Measure instead of assuming.** The Saans cough model is used on under-fives and was trained on adults, so it was evaluated by age band and the degradation reported rather than hidden. When a larger embedding model was proposed for the handbook assistant, three were benchmarked — the 440 MB candidates were *worse* on the question that already worked and did not fix the one that failed, so the 87 MB one shipped.

**Degrade rather than break.** No API key, no reranker, no network, no model weights — each of those paths has a defined fallback. An energy-based burst detector runs alongside the trained cough classifier so a model trained on adults cannot veto a small child's cough on its own.

**Read the dependency graph.** ChromaDB was rejected from Saans because it pulls a protobuf version that silently breaks the TensorFlow chest X-ray model; for a 264-page corpus the whole index is 1.7 MB and search is a dot product. TensorFlow is pinned below 2.16 because Keras 3 cannot build the sub-model Grad-CAM needs from a legacy `.h5`. Reasoning like that lives in the `requirements.txt`, where the next person will actually find it.

**Privacy is a default, not a setting.** Field data collection in Saans is off unless a deployment explicitly enables it, consent is confirmed per capture rather than per install, and nothing identifying is written to disk.

---

## Tools

**Languages** — Python · TypeScript · JavaScript · SQL

**ML** — TensorFlow/Keras · scikit-learn · DenseNet transfer learning · Grad-CAM · audio feature engineering (MFCC/spectral) · sentence-transformers · cross-encoder reranking · onnxruntime

**LLM systems** — RAG with local vector search · retrieval evaluation · multi-agent orchestration (CrewAI, LangChain) · multi-provider ensembles (Anthropic, OpenAI, Google) · MCP · prompt design with refusal guards

**Backend** — FastAPI · Express · SQLAlchemy · Drizzle ORM · PostgreSQL · SQLite · REST and streaming APIs

**Frontend** — React 19 · Vite · Tailwind · Radix/shadcn · TanStack Query · Streamlit · PWA, offline-first, i18n with RTL

**Infrastructure** — Docker & Compose · Cloudflare Tunnel · GitHub Actions · asset and model build pipelines

---

Open to internships and junior roles in ML engineering and applied AI.

[LinkedIn](https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/) · bbr70686@gmail.com
