<img src="assets/banner.png" width="100%" alt="Muhammad Abdullah — Applied ML & LLM Systems Engineer" />

<div align="center">

<a href="https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/"><img src="https://img.shields.io/badge/LinkedIn-0B1120?style=for-the-badge&logo=linkedin&logoColor=2DD4BF" alt="LinkedIn" /></a>&nbsp;
<a href="mailto:bbr70686@gmail.com"><img src="https://img.shields.io/badge/Email-0B1120?style=for-the-badge&logo=gmail&logoColor=2DD4BF" alt="Email" /></a>&nbsp;
<a href="https://github.com/ra189zor?tab=repositories"><img src="https://img.shields.io/badge/Repositories-0B1120?style=for-the-badge&logo=github&logoColor=2DD4BF" alt="Repositories" /></a>

</div>

<br/>

## 👋 &nbsp; About me

- 🎓 &nbsp; Final-year **Mechatronics** undergraduate (8th semester) in Hyderabad, Pakistan
- 🧠 &nbsp; I build **applied-ML and LLM systems end to end** — the model, the service around it, and the interface people actually use
- 🩺 &nbsp; Proudest of **[Saans](https://github.com/ra189zor/Saans)**, an offline-first paediatric TB-screening app built on the WHO 2022 clinical algorithm
- 🔍 &nbsp; I care most about the unglamorous parts — what happens when the model is wrong, the network drops, or the data is thinner than the claim
- 📫 &nbsp; Reach me on [LinkedIn](https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/) or at **bbr70686@gmail.com**

<br/>

## 🚀 &nbsp; Featured projects

### 🩺 &nbsp; [Saans](https://github.com/ra189zor/Saans) — offline paediatric TB screening

> An offline-first tablet app for community health workers, implementing the WHO Tuberculosis *Module 5 (2022)* decision algorithm. Three ML assists advise the health worker but can **never** override the clinical score.

- **Chest X-ray** — DenseNet121 + Grad-CAM over 13,265 films → **0.942 AUC**, 95.1% recall
- **Cough analysis** — RandomForest over 66 acoustic features, evaluated *by age band* rather than assumed
- **WHO assistant** — two-stage local retrieval (MiniLM → cross-encoder rerank) that cites a page or refuses
- Bilingual English / Urdu with full RTL · installable PWA · runs completely offline

&nbsp;&nbsp;&nbsp;&nbsp;![React](https://img.shields.io/badge/React_19-1E293B?style=flat-square&logo=react&logoColor=61DAFB) ![FastAPI](https://img.shields.io/badge/FastAPI-1E293B?style=flat-square&logo=fastapi&logoColor=009688) ![TensorFlow](https://img.shields.io/badge/TensorFlow-1E293B?style=flat-square&logo=tensorflow&logoColor=FF6F00) ![ONNX](https://img.shields.io/badge/ONNX_Runtime-1E293B?style=flat-square&logo=onnx&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-1E293B?style=flat-square&logo=docker&logoColor=2496ED)

### 🤖 &nbsp; AI-Powered Discord Automation Platform &nbsp;·&nbsp; *private*

> An event-driven Discord bot, an LLM interaction pipeline, and a FastAPI control panel running as one async application for a live community.

- **Treats the LLM as untrusted** — a 5-layer prompt-injection defence, output filtered before it ever ships, every attempt logged
- **Runs inside a free-tier budget** — thread-safe multi-key rotation + a token-budget manager that trims context instead of failing
- 5-layer context injection · function-calling long-term memory · async SQLite (WAL) · 11 scheduled background loops

&nbsp;&nbsp;&nbsp;&nbsp;![Python](https://img.shields.io/badge/Python-1E293B?style=flat-square&logo=python&logoColor=3776AB) ![discord.py](https://img.shields.io/badge/discord.py-1E293B?style=flat-square&logo=discord&logoColor=5865F2) ![FastAPI](https://img.shields.io/badge/FastAPI-1E293B?style=flat-square&logo=fastapi&logoColor=009688) ![SQLite](https://img.shields.io/badge/SQLite-1E293B?style=flat-square&logo=sqlite&logoColor=0AA9E6) ![asyncio](https://img.shields.io/badge/asyncio-1E293B?style=flat-square&logo=python&logoColor=3776AB)

**Also built**

- **[llm-observe-hub](https://github.com/ra189zor/llm-observe-hub)** — an OpenAI-compatible proxy that instruments local LLMs with cost, latency and alerts &nbsp;`FastAPI`
- **[WorkflowWizard](https://github.com/ra189zor/WorkflowWizard)** — turns plain-English descriptions into importable n8n workflow JSON &nbsp;`React` `TypeScript`
- **[fraud-detection-agent](https://github.com/ra189zor/fraud-detection-agent)** — Isolation Forest + a six-signal rule engine that learns from analyst feedback &nbsp;`scikit-learn`
- **[MCP-Studio](https://github.com/ra189zor/MCP-Studio)** — generates and validates MCP servers across three model providers in parallel &nbsp;`asyncio`

<br/>

## 🛠️ &nbsp; Tech stack

**Languages** &nbsp; ![Python](https://img.shields.io/badge/Python-2DD4BF?style=flat-square&logo=python&logoColor=0B1120) ![TypeScript](https://img.shields.io/badge/TypeScript-2DD4BF?style=flat-square&logo=typescript&logoColor=0B1120) ![JavaScript](https://img.shields.io/badge/JavaScript-2DD4BF?style=flat-square&logo=javascript&logoColor=0B1120) ![SQL](https://img.shields.io/badge/SQL-2DD4BF?style=flat-square&logo=postgresql&logoColor=0B1120)

**ML / Data** &nbsp; ![TensorFlow](https://img.shields.io/badge/TensorFlow-1E293B?style=flat-square&logo=tensorflow&logoColor=FF6F00) ![Keras](https://img.shields.io/badge/Keras-1E293B?style=flat-square&logo=keras&logoColor=D00000) ![scikit-learn](https://img.shields.io/badge/scikit--learn-1E293B?style=flat-square&logo=scikitlearn&logoColor=F7931E) ![ONNX](https://img.shields.io/badge/ONNX-1E293B?style=flat-square&logo=onnx&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-1E293B?style=flat-square&logo=numpy&logoColor=4DABCF) ![pandas](https://img.shields.io/badge/pandas-1E293B?style=flat-square&logo=pandas&logoColor=white)

**LLM** &nbsp; ![LangChain](https://img.shields.io/badge/LangChain-1E293B?style=flat-square&logo=langchain&logoColor=1C3C3C) ![CrewAI](https://img.shields.io/badge/CrewAI-1E293B?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-1E293B?style=flat-square) ![MCP](https://img.shields.io/badge/MCP-1E293B?style=flat-square&logo=anthropic&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-1E293B?style=flat-square&logo=openai&logoColor=white) ![Groq](https://img.shields.io/badge/Groq-1E293B?style=flat-square)

**Backend** &nbsp; ![FastAPI](https://img.shields.io/badge/FastAPI-1E293B?style=flat-square&logo=fastapi&logoColor=009688) ![Express](https://img.shields.io/badge/Express-1E293B?style=flat-square&logo=express&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-1E293B?style=flat-square&logo=postgresql&logoColor=4169E1) ![SQLite](https://img.shields.io/badge/SQLite-1E293B?style=flat-square&logo=sqlite&logoColor=0AA9E6) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-1E293B?style=flat-square&logo=sqlalchemy&logoColor=white)

**Frontend & Infra** &nbsp; ![React](https://img.shields.io/badge/React-1E293B?style=flat-square&logo=react&logoColor=61DAFB) ![Vite](https://img.shields.io/badge/Vite-1E293B?style=flat-square&logo=vite&logoColor=646CFF) ![Tailwind](https://img.shields.io/badge/Tailwind-1E293B?style=flat-square&logo=tailwindcss&logoColor=06B6D4) ![Streamlit](https://img.shields.io/badge/Streamlit-1E293B?style=flat-square&logo=streamlit&logoColor=FF4B4B) ![Docker](https://img.shields.io/badge/Docker-1E293B?style=flat-square&logo=docker&logoColor=2496ED)

<br/>

## 📊 &nbsp; GitHub

<div align="center">

<img height="165" src="https://github-readme-stats-eight-theta.vercel.app/api?username=ra189zor&show_icons=true&include_all_commits=true&count_private=true&hide_border=true&bg_color=00000000&title_color=2DD4BF&icon_color=2DD4BF&text_color=8595AD" alt="GitHub stats" />
&nbsp;&nbsp;
<img height="165" src="https://streak-stats.demolab.com/?user=ra189zor&hide_border=true&background=00000000&stroke=1E293B&ring=2DD4BF&fire=2DD4BF&currStreakLabel=2DD4BF&currStreakNum=F1F5F9&sideLabels=8595AD&sideNums=F1F5F9&dates=475569&excludeDaysLabel=475569" alt="Contribution streak" />

</div>

<br/>

## 🤝 &nbsp; Connect

<div align="center">

**Open to internships and junior roles in ML engineering and applied AI.**

<a href="https://www.linkedin.com/in/abdullah-kaimkhani-09b1292b9/"><img src="https://img.shields.io/badge/LinkedIn-0B1120?style=for-the-badge&logo=linkedin&logoColor=2DD4BF" alt="LinkedIn" /></a>&nbsp;
<a href="mailto:bbr70686@gmail.com"><img src="https://img.shields.io/badge/Email-0B1120?style=for-the-badge&logo=gmail&logoColor=2DD4BF" alt="Email" /></a>

</div>
