# Johnathan Carrizales

Full-stack engineer focused on AI-backed products: RAG pipelines, mobile and web apps, and the automation that keeps them running. B.S. Computer Science (Math minor), Texas State University, Magna Cum Laude.

[LinkedIn](https://linkedin.com/in/johnathanECarr) · JohnathanE.Carrizales@gmail.com

---

## Work at Bear Creek AI (Feb 2026 – Jul 2026)

Full-Stack Engineer I on KnowledgeXpert, a RAG platform for searching regulatory and technical documents. The code lives in private company repositories, so this section describes what I built rather than linking to it. No proprietary code or configuration is included here.

Contribution activity on my Bear Creek AI work account (private repos), Mar–Jul 2026:

<img width="1079" height="498" alt="image" src="https://github.com/user-attachments/assets/6118b105-dac5-4c55-a936-746c41067fc2" />



### Automated knowledge-base update pipeline (GitHub Actions)
**Problem:** Regulatory sources publish new documents on their own schedules, and the knowledge bases were going stale between manual refreshes.

**What I built:** A standalone repository I designed and owned end to end. Scheduled GitHub Actions workflows run a set of update scripts (grew from 4 to 9+ sources across PHMSA, FAA, NTSB, and EPA TSCA) that detect new documents, download them, and upload them to the platform's ingestion API.
- Secrets resolved env-first with a secrets-manager fallback (Infisical), so the same scripts run in CI, in Docker, and locally
- Service-to-service auth via internal token headers
- Fixed a Docker secret-injection bug and a stale date-cutoff bug that was silently skipping documents
- Rebuilt a scraper after a source site restructured its data model
- Local test path that exercises detection and download without touching production

**Stack:** Python, GitHub Actions, Docker, Infisical, MongoDB

### Production RAG ingestion and retrieval pipeline
**Problem:** Each new knowledge base was built by hand, slowly and inconsistently.

**What I built:** An ingestion and retrieval pipeline, then used it to source, build, and QA 20+ regulatory knowledge bases end to end (FDA 510(k) and De Novo, PHMSA, FAA, OSHA, REACH/RoHS, CAS Registry, and NAICS-sector KBs). I owned the full marketplace catalog.
- Document parsing, chunking, OpenAI embeddings, and vector indexing in Pinecone and MongoDB Atlas Vector Search
- Retrieval tool built with LangChain: hybrid lookup plus semantic search, with Cohere reranking
- Source files stored in Azure Blob Storage for the in-app PDF viewer; diagnosed and fixed a storage-account mismatch that broke it
- Deduplication pass across MongoDB and Pinecone after re-ingestion
- Validity testing to confirm the system returned correct, grounded answers
- Finding I documented: RAG is a poor fit for large tabular datasets, which need a text-to-SQL hybrid instead

**Stack:** Python, LangChain, OpenAI API, Pinecone, MongoDB Atlas, Azure Blob Storage, Cohere

### React Native mobile app (Android/iOS)
**Problem:** The platform was web-only.

**What I built:** The mobile app from the ground up, with coordinated changes across 4 repositories (app, auth service, KB service, prompt service).
- Token-based auth designed end to end: Bearer tokens stored in the device keychain
- Streaming chat responses, knowledge-base selection, chat history, follow-up suggestions, and a model selector
- Authenticated PDF downloads with native preview
- Android share extension so users can send documents into the app from other apps
- Security hardening from a code-scanning audit: HTTPS-only network config and removal of insecure local-networking exceptions

**Stack:** React Native (New Architecture), TypeScript, Kotlin, Node.js

### Marketplace monorepo extraction and deployment
**Problem:** The marketplace shared repositories with two unrelated services, so local setup pulled in everything and deploys were coupled.

**What I built:** Extracted it into a standalone monorepo housing both its frontend and backend.
- Local setup reduced to the marketplace's own dependencies
- Independent deploys: frontend on Cloudflare Pages, backend on Koyeb, each with production and preview environments
- Environment-specific configuration, including private npm package auth in both environments and a dev-only auth bypass gated by environment
- Built a deep-link flow that pre-selects a knowledge base when a user arrives from the marketplace (4 PRs across 3 repos)

**Stack:** React, Vite, Node.js, Cloudflare Pages, Koyeb

### Role-based access control migration
**Problem:** Access was controlled by a single boolean flag, and knowledge-base access rules were hardcoded.

**What I built:**
- Replaced the boolean with a role field across five services and migrated every existing user, with zero downtime
- Replaced hardcoded KB access logic with a config-driven resolution system
- Added a developer role that bypasses rate limits and usage entitlements, with a 5-minute TTL cache to avoid a database lookup on every request

**Stack:** Python, FastAPI, MongoDB

### Manufacturer catalog ingestion
Built 25+ scrapers that collected product documentation from industrial electrical manufacturers to populate shared knowledge bases. All of them follow one pattern: checkpoint and resume, manifests, bounded async concurrency, exponential backoff, and JSONL output.

**Stack:** Python, Playwright, BeautifulSoup, asyncio

### LLM and vector database cost analysis
Wrote a unit-economics report for the VP of Engineering covering parsing (LlamaParse), storage (Azure), and vector database (Pinecone) costs, with per-file and per-page breakdowns and projections for upcoming knowledge bases.

---

## Personal projects

### [Resume Studio: AI Resume & Cover Letter Generator](https://github.com/JohnathanCarr/resume-cv-generator)
Chrome extension (Manifest V3) that tailors a user's own resume to a job posting and writes a matching cover letter. It reads the posting against the user's profile, flags missing ATS keywords for the user to confirm, and returns the resume as a validated list of edits planned to fit one page, highlighted in the preview and exported as a text PDF. Runs entirely in the browser with the user's own OpenAI key; no backend. Started as a cover-letter-only tool; extended using Claude for AI-assisted development.
- Structured outputs with no-fabrication rules: every claim must trace back to the profile or a cited source
- Unit tests (node:test) for the generation helpers, plus a prompt eval set (profiles × job postings, scored by rubric) run before every prompt change

**Stack:** JavaScript, Chrome Extensions (MV3), OpenAI API, pdf.js, jsPDF, node:test

### Crash Severity Prediction
Cleaned and analyzed 190K+ Texas crash records, then trained Random Forest and Logistic Regression models to infer severity for crashes recorded as unknown. Reduced false negatives by 60%, evaluated with precision-recall curves and F1.
**Stack:** Python, Pandas, scikit-learn, TensorFlow

### [Connect Four AI](https://github.com/JohnathanCarr/minimax-connect4)
Playable Connect Four against an AI using Minimax with alpha-beta pruning and a custom defensive evaluation function. Logs nodes expanded, move time, and memory use per game.
**Stack:** Python, Pygame

---

## Skills

- **Languages:** Python, JavaScript, TypeScript, C++
- **Frontend & Mobile:** React, React Native, Vite
- **Backend:** Node.js, Express, FastAPI, REST APIs, JWT auth, RBAC
- **Databases:** MongoDB (Atlas, PyMongo), Pinecone, Atlas Vector Search
- **AI/ML:** OpenAI API, LangChain, Cohere Rerank, RAG, scikit-learn, TensorFlow, PyTorch
- **DevOps & Cloud:** GitHub Actions, Docker, Azure Blob Storage, Cloudflare Pages, Koyeb, Infisical
- **Tools:** Git/GitHub, Jira, VS Code, Claude for AI-assisted development
