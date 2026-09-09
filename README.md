<div align="center">

# `SYSTEM : MUHAMMAD ABDULLAH`

```yaml
type: Applied ML & LLM Systems Engineer
status: Final-year Mechatronics · 8th semester
location: Hyderabad, Pakistan
```

<a href="https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/">
<img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="mailto:bbr70686@gmail.com">
<img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
<img src="https://img.shields.io/badge/Hyderabad,_PK-1F6FEB?style=for-the-badge&logo=googlemaps&logoColor=white" alt="Location" />

</div>

---

## System Identity

I build applied-ML and LLM systems end to end — train the model, wrap it in a service that fails gracefully, and put a real interface in front of it. The part I care most about is what happens when the model is wrong, the network is gone, or the data is thinner than the claim.

Most of what follows is about that.

---

## Architecture Overview

```mermaid
flowchart TB
    subgraph INPUT [ Input Layer ]
        direction LR
        D1["13,265 chest X-rays"]
        D2["1,055 WHO handbook passages"]
        D3["Cough audio + acoustic features"]
        D4["Live Discord community traffic"]
    end

    subgraph CORE [ Processing Pipeline ]
        direction LR
        P1["ML Training + Grad-CAM"]
        P2["LLM System Design"]
        P3["Service Layer + Graceful Degradation"]
    end

    subgraph OUTPUT [ Output Layer ]
        direction LR
        O1["Production Systems"]
        O2["Honest Benchmarks"]
        O3["Fail-safe Defaults"]
    end

    INPUT --> CORE --> OUTPUT

    classDef input fill:#0D1117,stroke:#0D9488,color:#0D9488
    classDef proc fill:#0D1117,stroke:#2F81F7,color:#2F81F7
    classDef output fill:#0D1117,stroke:#F97316,color:#F97316
    class D1,D2,D3,D4 input
    class P1,P2,P3 proc
    class O1,O2,O3 output
```

> **Cross-cutting concerns applied to every layer:**
> Security · Privacy by default · Observability · Graceful degradation

---

## Subsystems

### `01` Saans — Paediatric TB Screening

> Offline-first tablet app for community health workers implementing the WHO *Operational Handbook on Tuberculosis, Module 5* (2022) decision algorithm. Three ML assists inform the health worker and are **structurally prevented** from changing the score.

```mermaid
flowchart LR
    subgraph pipeline [ Screening Pipeline ]
        direction LR
        A["Chest X-ray\nDenseNet121"] --> F["Clinical\nScore"]
        B["Cough Audio\n66 features"] --> F
        C["WHO Handbook\nRAG + Rerank"] --> F
        F --> G["Health Worker\nDecision"]
    end

    style pipeline fill:#0D1117,stroke:#0D9488,color:#0D9488
```

| Metric | Value | Detail |
|:--|:--|:--|
| **AUC** | `0.942` | honest single-site benchmark |
| **Recall** | `95.1%` | 271 of 285 TB cases |
| **Specificity** | `98.2%` | 30 false alarms / 1,705 |
| **Dataset** | `13,265` | 4 sources, hash-deduped |

> **The reported AUC is 0.942, not the 0.995 the pooled test set produces.** One source draws its TB and normal films from different collections that differ for reasons unrelated to disease, so the model separates them without reading pathology. The honest benchmark is the single hospital where both classes share equipment. Quoting the inflated number would have been easy, and wrong.

**Technical detail.** Two-stage local retrieval — MiniLM bi-encoder on ONNX Runtime, then cross-encoder rerank, ~3 ms, refusing before it ever calls an API. No public paediatric dataset exists, so every model was trained on adults and scored *by age band* rather than assumed to transfer. Bilingual EN/UR with full RTL, installable PWA, fully offline.

<img src="https://img.shields.io/badge/React_19-20232A?style=flat-square&logo=react" height="22" /> <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat-square&logo=onnx&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="22" />

**[-> Read the code and the limitations](https://github.com/ra189zor/Saans)** &nbsp; <img src="https://img.shields.io/github/last-commit/ra189zor/Saans?style=flat-square&label=last%20commit&color=30363D&labelColor=30363D" height="20" />

---

### `02` Discord AI Platform — Automation and Security

> Event-driven Discord bot + LLM interaction pipeline + FastAPI control panel, running as one async application. Closed-source — engineering described, not linked.

```mermaid
flowchart LR
    subgraph flow [ Request Lifecycle ]
        direction LR
        A["User Input"] --> B["5 Defence\nLayers"]
        B --> C["LLM + 5 Context\nLayers"]
        C --> D["Output\nFilter"]
        D --> E["Response"]
        B -.-> F["Security\nLog"]
        D -.-> F
    end

    style flow fill:#0D1117,stroke:#7C3AED,color:#7C3AED
```

| Metric | Value | Detail |
|:--|:--|:--|
| **Defence layers** | `5` | against prompt injection |
| **Context layers** | `5` | injected per LLM call |
| **Background loops** | `11` | scheduled + cache refresh |
| **Slash commands** | `37` | across 6 subsystems |

> **Treating the LLM as untrusted, in both directions.** User input is delimiter-wrapped and pre-filtered for jailbreak patterns; tools are sandboxed with zero `eval`/`exec` and every query partitioned by guild; generated output is post-filtered for system-prompt leakage before it reaches anyone. Blocked inputs and leaked outputs are both written to a security log the admin panel surfaces — an attack surface you can actually watch.

**Engineering highlights.** Thread-safe multi-key rotation pool reads `x-ratelimit-remaining-*` headers off every response to rotate *before* limits land, and honours `retry-after` cooldowns on 429. Token budget manager trims conversation history and drops tool definitions dynamically to stay under the per-minute ceiling instead of failing with a 413. Five-layer context injection per call, LLM function calling for persistent memory, async SQLite on `aiosqlite` (WAL, startup migrations, `contextvars`-scoped connections), internal HTTP API for bot-dashboard IPC, fails-closed feature flags, and a Pillow canvas renderer for generated cards.

<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/discord.py-5865F2?style=flat-square&logo=discord&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/asyncio-3776AB?style=flat-square&logo=python&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="22" />

---

### Supporting Systems

```mermaid
flowchart LR
    subgraph supporting [ Additional Components ]
        direction TB
        L["llm-observe-hub\nObservability proxy for local LLMs\nFastAPI · SQLAlchemy · httpx"]
        W["WorkflowWizard\nNL to n8n workflow JSON\nReact · TypeScript · Drizzle · Neon"]
        M["MCP-Studio\nMulti-model MCP validator\nasyncio · PostgreSQL · Streamlit"]
        L --- W --- M
    end

    style supporting fill:#0D1117,stroke:#30363D,color:#8B949E
```

<sub>**[MindFlow](https://github.com/ra189zor/MindFlow)** and **[JobNexus](https://github.com/ra189zor/JobNexus)** are where the multi-agent pattern I keep reaching for got worked out: specialist agents behind a validator that checks their output against the original constraints and returns it for revision until it passes or hits a cap. Also built: **[fraud-detection-agent](https://github.com/ra189zor/fraud-detection-agent)** — hybrid Isolation Forest / One-Class SVM with a six-signal rule engine; **[AI-Venture-Capital-Scout](https://github.com/ra189zor/AI-Venture-Capital-Scout)** — CrewAI agent crew paired with a TensorFlow founder-success model.</sub>

---

## Tech Stack

```mermaid
flowchart TB
    subgraph ml [ ML and Vision ]
        direction LR
        TensorFlow --- Keras --- scikit-learn --- ONNX --- NumPy --- pandas
    end

    subgraph llm [ LLM Systems ]
        direction LR
        RAG --- LangChain --- CrewAI --- MCP --- OpenAI --- Groq
    end

    subgraph be [ Backend ]
        direction LR
        Python --- FastAPI --- Express --- PostgreSQL --- SQLite --- SQLAlchemy
    end

    subgraph fe [ Frontend and Infra ]
        direction LR
        React --- TypeScript --- Vite --- Tailwind --- Streamlit --- Docker
    end

    ml --> llm --> be --> fe

    classDef layer fill:#0D1117,stroke:#30363D,color:#C9D1D9
    class ml,llm,be,fe layer
```

---

## Operational Principles

```mermaid
stateDiagram-v2
    [*] --> Nominal

    Nominal --> Fallback : dependency fails
    Fallback --> Nominal : recovered
    Fallback --> Degraded : cascading failure
    Degraded --> Fallback : partial recovery
    Degraded --> SafeState : all fallbacks exhausted
    SafeState --> Nominal : manual intervention

    note right of Nominal : All systems operational
    note right of Degraded : Reduced capability, no crash
    note right of SafeState : Fails closed, never open
```

| # | Principle | Evidence |
|:--|:--|:--|
| `01` | **Measure instead of assuming** | Cough model scored by age band since it was trained on adults. Three embedding models benchmarked — the 440 MB candidates were *worse*, so the 87 MB one shipped. |
| `02` | **Degrade, don't break** | No API key, no reranker, no network, no model weights, no rate-limit headroom — each has a defined fallback. Energy-based burst detector runs beside the trained classifier. |
| `03` | **Read the dependency graph** | ChromaDB rejected because its protobuf silently breaks TensorFlow. TF pinned below 2.16 because Keras 3 cannot build the Grad-CAM sub-model. Reasoning lives in `requirements.txt`. |
| `04` | **Safe and private by default** | Field data collection off by default, consent per capture, nothing identifying written. Feature flags fail closed. LLM output filtered before reaching any user. |

---

## Endpoints

```yaml
GET /contact:
  - type: LinkedIn
    uri: https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/
  - type: Email
    uri: bbr70686@gmail.com
  - type: Repositories
    uri: https://github.com/ra189zor?tab=repositories
```

> **Open to internships and junior roles in ML engineering and applied AI** — happy to talk through any of the work above, including the parts that didn't work.

<a href="https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/">
<img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="mailto:bbr70686@gmail.com">
<img src="https://img.shields.io/badge/bbr70686@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
<a href="https://github.com/ra189zor?tab=repositories">
<img src="https://img.shields.io/badge/All_repositories-181717?style=for-the-badge&logo=github&logoColor=white" alt="Repositories" /></a>

<sub>
<img src="https://img.shields.io/github/followers/ra189zor?style=flat-square&logo=github&label=followers&color=30363D&labelColor=30363D" height="20" />
<img src="https://img.shields.io/github/last-commit/ra189zor/Saans?style=flat-square&label=last%20push&color=30363D&labelColor=30363D" height="20" />
</sub>
