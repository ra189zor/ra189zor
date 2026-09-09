<div align="center">

<img src="https://github.com/user-attachments/assets/9a8e3477-0475-4a96-82cb-b010d54741f9" alt="Muhammad Abdullah — AI Developer, Python Innovator, Multi-Agent Specialist" width="100%" />

<br/><br/>

<a href="https://github.com/ra189zor">
<img src="https://readme-typing-svg.demolab.com/?lines=DenseNet121%20%2B%20Grad-CAM%20over%2013%2C265%20chest%20X-rays;Two-stage%20local%20RAG%20with%20cross-encoder%20reranking;Five-layer%20prompt-injection%20defence%2C%20in%20production;Multi-agent%20pipelines%20that%20validate%20their%20own%20output&font=JetBrains%20Mono&weight=500&size=17&pause=1200&color=2F81F7&center=true&vCenter=true&width=620&height=45" alt="What I build" />
</a>

<br/>

<a href="https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/">
<img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="mailto:bbr70686@gmail.com">
<img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
<img src="https://img.shields.io/badge/Hyderabad,_Pakistan-1F6FEB?style=for-the-badge&logo=googlemaps&logoColor=white" alt="Location" />

</div>

<br/>

## Muhammad Abdullah

**Final-year Mechatronics student, 8th semester.** I build applied-ML and LLM systems end to end — train the model, wrap it in a service that fails gracefully, and put a real interface in front of it.

The part I care most about is what happens when the model is wrong, the network is gone, or the data is thinner than the claim. Most of what follows is about that.

---

## Featured

### <img src="https://img.shields.io/badge/Healthcare_ML-0D9488?style=flat-square" height="20" /> Saans — paediatric TB screening for community health workers

An offline-first tablet app implementing the WHO *Operational Handbook on Tuberculosis, Module 5* (2022) decision algorithm. Three ML assists inform the health worker and are **structurally prevented** from changing the score.

<table>
<tr>
<td align="center" width="25%" valign="top"><h2>0.942</h2><sub><b>AUC</b><br/>honest single-site benchmark</sub></td>
<td align="center" width="25%" valign="top"><h2>95.1%</h2><sub><b>Recall</b><br/>271 of 285 TB cases</sub></td>
<td align="center" width="25%" valign="top"><h2>98.2%</h2><sub><b>Specificity</b><br/>30 false alarms / 1,705</sub></td>
<td align="center" width="25%" valign="top"><h2>13,265</h2><sub><b>X-rays</b><br/>4 sources, hash-deduped</sub></td>
</tr>
</table>

> **The reported AUC is 0.942, not the 0.995 the pooled test set produces.** One source draws its TB and normal films from different collections that differ for reasons unrelated to disease, so the model separates them without reading pathology. The honest benchmark is the single hospital where both classes share equipment. Quoting the inflated number would have been easy, and wrong.

**DenseNet121 + Grad-CAM** for films · **RandomForest over 66 acoustic features** for cough · **two-stage local retrieval** over 1,055 handbook passages — MiniLM, then a cross-encoder rerank, ~3 ms, refusing before it ever calls an API.

Every model was trained on adults, because no public paediatric dataset exists — so every under-18 recording was held out and the model scored *by age band* rather than assumed to transfer. Bilingual EN/UR with RTL, installable PWA, fully offline.

<img src="https://img.shields.io/badge/React_19-20232A?style=flat-square&logo=react" height="22" /> <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat-square&logo=onnx&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="22" />

**[→ Read the code and the limitations](https://github.com/ra189zor/Saans)** &nbsp; <img src="https://img.shields.io/github/last-commit/ra189zor/Saans?style=flat-square&label=last%20commit&color=30363D&labelColor=30363D" height="20" />

<br/>

### <img src="https://img.shields.io/badge/Private-6E7681?style=flat-square" height="20" /> AI-Powered Discord Automation & Community Platform

A production companion service for a live community: an event-driven Discord bot, an LLM interaction pipeline, and a FastAPI control panel, running as one async application. Closed-source, so the engineering is described rather than linked.

<table>
<tr>
<td align="center" width="25%" valign="top"><h2>5</h2><sub><b>Defence layers</b><br/>against prompt injection</sub></td>
<td align="center" width="25%" valign="top"><h2>5</h2><sub><b>Context layers</b><br/>injected per LLM call</sub></td>
<td align="center" width="25%" valign="top"><h2>11</h2><sub><b>Background loops</b><br/>scheduled + cache refresh</sub></td>
<td align="center" width="25%" valign="top"><h2>37</h2><sub><b>Slash commands</b><br/>across 6 subsystems</sub></td>
</tr>
</table>

> **Treating the LLM as untrusted, in both directions.** User input is delimiter-wrapped and pre-filtered for jailbreak patterns; tools are sandboxed with zero `eval`/`exec` and every query partitioned by guild; generated output is post-filtered for system-prompt leakage before it reaches anyone. Blocked inputs and leaked outputs are both written to a security log the admin panel surfaces — an attack surface you can actually watch.

**Running an LLM inside a free-tier budget** turned out to be the real engineering. A thread-safe multi-key rotation pool reads `x-ratelimit-remaining-*` headers off every response to rotate *before* limits land, and honours `retry-after` cooldowns on 429. A token budget manager trims conversation history and drops tool definitions dynamically to stay under the per-minute ceiling instead of failing with a 413.

Around that: five-layer context injection per call, **LLM function calling** for persistent memory and verified moderation actions, async SQLite on `aiosqlite` (WAL, startup migrations, `contextvars`-scoped connections), an internal HTTP API for bot↔dashboard IPC, fails-closed feature flags, and a Pillow renderer for generated cards.

<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/discord.py-5865F2?style=flat-square&logo=discord&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/asyncio-3776AB?style=flat-square&logo=python&logoColor=white" height="22" /> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="22" />

---

## Also built

| | Project | What it is |
|:--|:--|:--|
| <img src="https://img.shields.io/github/stars/ra189zor/llm-observe-hub?style=flat-square&label=%E2%98%85&color=1F6FEB&labelColor=1F6FEB" height="18" /> | **[llm-observe-hub](https://github.com/ra189zor/llm-observe-hub)** | An OpenAI-compatible **proxy** that sits in front of local LLMs and instruments them — streaming pass-through, per-request cost and latency logging, a configurable alert engine, budgets and model comparison. Observability as a sidecar, not a library you import. <br/> <sub>`FastAPI` `SQLAlchemy` `httpx`</sub> |
| | **[WorkflowWizard](https://github.com/ra189zor/WorkflowWizard)** | Plain-English automation descriptions → validated, importable n8n workflow JSON. Built as a product, not a demo: session auth, Postgres persistence, subscription billing, usage metering. <br/> <sub>`React` `TypeScript` `Express` `Drizzle` `Neon Postgres`</sub> |
| | **[fraud-detection-agent](https://github.com/ra189zor/fraud-detection-agent)** | Hybrid transaction scoring — Isolation Forest / One-Class SVM alongside a six-signal rule engine (amount, merchant, geography, velocity, timing, device). Analyst feedback retrains the model; an LLM writes the explanation. <br/> <sub>`scikit-learn` `Streamlit` `SQLite`</sub> |
| | **[MCP-Studio](https://github.com/ra189zor/MCP-Studio)** | Generates and validates MCP server implementations, fanning one task across Anthropic, OpenAI and Google models in parallel and reconciling the output. Ships a code validator and test harness. <br/> <sub>`asyncio` `PostgreSQL` `Streamlit`</sub> |
| | **[AI-Venture-Capital-Scout](https://github.com/ra189zor/AI-Venture-Capital-Scout)** | Startup screening pairing a CrewAI agent crew with a TensorFlow founder-success model trained separately, plus document ingestion and market saturation scoring. <br/> <sub>`CrewAI` `LangChain` `TensorFlow`</sub> |

<sub>**[MindFlow](https://github.com/ra189zor/MindFlow)** and **[JobNexus](https://github.com/ra189zor/JobNexus)** are where the multi-agent pattern I keep reaching for got worked out: specialist agents behind a validator that checks their output against the original constraints and returns it for revision until it passes or hits a cap.</sub>

---

## How I build

<table>
<tr>
<td width="50%" valign="top">

**Measure instead of assuming**

The cough model runs on under-fives and was trained on adults, so it was scored by age band and the degradation published. Three embedding models were benchmarked for the handbook assistant — the 440 MB candidates were *worse* on the question that already worked, so the 87 MB one shipped.

</td>
<td width="50%" valign="top">

**Degrade, don't break**

No API key, no reranker, no network, no model weights, no rate-limit headroom — each of those has a defined fallback. An energy-based burst detector runs beside the trained cough classifier so an adult-trained model can't veto a small child's cough alone.

</td>
</tr>
<tr>
<td width="50%" valign="top">

**Read the dependency graph**

ChromaDB was rejected from Saans because it pulls a protobuf version that silently breaks the TensorFlow X-ray model. TensorFlow is pinned below 2.16 because Keras 3 can't build the sub-model Grad-CAM needs from a legacy `.h5`. That reasoning lives in `requirements.txt`, where the next person will find it.

</td>
<td width="50%" valign="top">

**Safe and private by default**

Field data collection is off unless a deployment enables it, consent is per capture rather than per install, and nothing identifying is written. Feature flags fail closed. LLM output is filtered before it reaches a user, and both directions are logged.

</td>
</tr>
</table>

---

## Stack

**ML & Vision** &nbsp;
<img src="https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Keras-D00000?style=flat-square&logo=keras&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat-square&logo=onnx&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white" height="24" />

**LLM systems** &nbsp;
<img src="https://img.shields.io/badge/RAG_+_reranking-2F81F7?style=flat-square" height="24" />
<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/CrewAI-FF5A5F?style=flat-square" height="24" />
<img src="https://img.shields.io/badge/MCP-000000?style=flat-square&logo=anthropic&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Groq-F55036?style=flat-square" height="24" />

**Backend** &nbsp;
<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat-square&logo=sqlalchemy&logoColor=white" height="24" />

**Frontend & Infra** &nbsp;
<img src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react" height="24" />
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white" height="24" />
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="24" />

---

## Connect

**Open to internships and junior roles in ML engineering and applied AI** — happy to talk through any of the work above, including the parts that didn't work.

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
