# Awesome-Resume-Parsing-Candidate-Screening

# Awesome Resume Parsing & Candidate Screening

> A curated list of top Resume Parsing and Candidate Screening platforms — both SaaS/Hosted commercial solutions and open-source alternatives for extracting structured data from resumes, matching candidates to job descriptions, and automating initial screening workflows.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Textkernel](#textkernel)
  - [Daxtra](#daxtra)
  - [Sovren (now part of Talenteca)](#sovren-now-part-of-talenteca)
  - [RChilli](#rchilli)
  - [Affinda](#affinda)
  - [HireAbility](#hireability)
- [Open-Source Software](#-open-source-software)
  - [SmartResume (Alibaba)](#smartresume-alibaba)
  - [CandiSift](#candisift)
  - [resume-extract](#resume-extract)
  - [resume-parser-ats](#resume-parser-ats)
  - [CVInsight](#cvinsight)
  - [Resume Analyzer Agent](#resume-analyzer-agent)
  - [SmartHire](#smarthire)
  - [HireFlow](#hireflow)
  - [OpenCATS](#opencats)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Resume Parsing and Candidate Screening platforms. These are not open-source but are included as reference points for feature comparison.

### Textkernel
**Type:** Enterprise resume parsing with taxonomy-driven normalization
Textkernel is one of the long-standing enterprise standards for resume parsing, with a deep investment in taxonomy-driven normalization that keeps search results clean over time [citation:4][citation:10]. It supports 29+ languages and bundles semantic search and matching capabilities alongside parsing. Pricing is quote-based, typically targeting larger recruiting organizations and staffing firms.

### Daxtra
**Type:** Resume parsing with semantic search and matching
Daxtra provides resume parsing with semantic search and matching, supporting multiple languages and offering taxonomy-driven normalization similar to Textkernel [citation:4][citation:10]. It is often evaluated alongside Textkernel and Sovren for enterprise recruiting stacks, with quote-based pricing.

### Sovren (now part of Talenteca)
**Type:** Resume parsing with multi-language support
Sovren has invested years in resume parsing technology and supports multiple languages [citation:4]. It is frequently cited as one of the established commercial parsers alongside Textkernel and Daxtra, though its ownership has changed over time. Pricing is quote-based.

### RChilli
**Type:** API-first resume parsing with broad language support
RChilli is an API-first resume parser supporting 40+ languages, with taxonomy-driven normalization and semantic search capabilities [citation:4][citation:10]. It gives developers control over extraction but requires engineering time to integrate. Pricing is usage-based or annual bundles.

### Affinda
**Type:** Resume parsing with self-hosting option
Affinda supports 50+ languages (the broadest among commercial parsers per one comparison [citation:4]) and is notable for offering **self-hosting**, which most competitors do not [citation:10]. It bundles semantic search and matching alongside parsing, with usage-based APIs starting around $0.10 per parse and annual bundles from $800 for 6,000 parses [citation:10]. It is ISO/SOC 2 compliant for cloud processing.

### HireAbility
**Type:** Long-standing US-based resume parsing
HireAbility is a smaller US company founded in 1999 with proven parsing technology, though its integration ecosystem is narrower than Affinda's or RChilli's [citation:10]. Pricing is quote-based, targeting enterprises that value a long track record over modern API extensibility.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Resume Parsing and Candidate Screening tools. The open-source ecosystem spans **layout-aware LLM parsers**, **full ATS platforms with bias auditing**, **lightweight local extractors**, and **AI-powered matching engines**.

### SmartResume (Alibaba)
**Stack:** Python / LLM / OCR | **License:** Open Source (compliance refactored)
SmartResume is a **layout-aware resume parsing system** from Alibaba that ingests PDF, image, and Office formats, extracts clean text via OCR and PDF metadata, reconstructs reading order with layout detection, and leverages LLMs to convert content into structured fields [citation:1]. It reports **93.1% overall extraction accuracy**, 92.1% layout detection mAP@0.5, and **1.22s single-page processing time**, with support for many languages [citation:1]. It supports local model deployment via vLLM (Qwen-0.6B-resume) to avoid external API dependencies. **Important note:** Due to open-source compliance, internal PDF parsing and OCR components were replaced with open-source alternatives, so some features may not fully match the original implementation [citation:1].  
**Best for:** Teams wanting a high-accuracy, layout-aware parser with LLM extraction and local model deployment, accepting the compliance-related refactoring caveats.

### CandiSift
**Stack:** Python / FastAPI / SQLite / LLM (Agno/Claude) | **License:** Open Source
CandiSift is an **open-source AI ATS** with LLM resume screening, CV parsing, JD-to-candidate matching, and **bias-audited ranking** [citation:2]. Key features include:
- **Deterministic hard filters** (auth, location, years, certs) run pre-LLM to avoid unnecessary costs 
- **Persona agents** (Technical + Risk in parallel) with **evidence-cited** scoring 
- **PII stripped before any model sees a candidate**, with an append-only audit log and a **bias-audit endpoint** 
- **Durable queue** with SQLite, retry/backoff, circuit breaker per model, and dead-letter handling 
- **ATS-readability scoring** and near-duplicate/resume-farming detection (Jaccard) 

It uses SOLID architecture with swappable adapters (stub/Agno/resilient providers), runs offline with a stub provider, and includes a recruiter UI with ranked table and accept/reject [citation:2].  
**Best for:** Teams wanting a privacy-first, bias-auditable AI screening pipeline with production-minded resilience patterns, accepting a younger project with SQLite persistence.

### resume-extract
**Stack:** TypeScript / ONNX (DistilBERT) | **License:** Open Source
resume-extract is a **fast, fully local resume extraction library** using a fine-tuned DistilBERT NER model exported to ONNX [citation:11]. It extracts name, email, phone, location, companies, titles, education, skills, seniority, country, and experience years, with **~15ms per resume** after model load and **no API calls** [citation:11]. It supports PDF (via Kreuzberg, optional Tesseract/EasyOCR/PaddleOCR) and DOCX, and includes an ATS completeness score. Model metrics include **97.77% entity F1** on clean resumes and 69.24% on noisy/OCR text, with a 63MB quantized model [citation:11].  
**Best for:** Developers wanting blazing-fast, offline resume extraction with strong structured output and zero external dependencies, accepting a fixed model (no LLM) and English-centric performance.

### resume-parser-ats
**Stack:** TypeScript / Node.js | **License:** Open Source
resume-parser-ats is a **CLI and MCP server** that deeply parses resumes using the OpenResume 4-step algorithm, evaluates **ATS compatibility** (A+ to F grading with per-field confidence), and provides prioritized, actionable improvement suggestions [citation:5]. It extracts 10+ fields from raw text or PDF, runs **entirely locally with no proprietary API calls**, and supports configurable strictness (lenient/moderate/strict) [citation:5]. The MCP server exposes `parse_resume`, `analyze_resume`, and `suggest_improvements` tools for AI agent integration.  
**Best for:** Developers and job seekers wanting local ATS scoring and improvement suggestions with MCP accessibility, accepting a focus on ATS readability rather than deep semantic matching.

### CVInsight
**Stack:** Python / Gemini LLM | **License:** Open Source
CVInsight is a Python library that extracts structured data from resumes using Google's Gemini models, with dedicated methods for `extract_profile`, `extract_education`, `extract_experience`, `extract_skills`, and `extract_years_of_experience` [citation:14]. It provides both a `CVInsightClient` class and a CLI, with configurable model selection and token usage logging. **Trade-off:** It depends on Gemini API keys (cloud LLM), so data leaves the local environment unless you swap providers.  
**Best for:** Python developers wanting a straightforward, LLM-powered extraction library with granular extraction methods, accepting the Gemini API dependency.

### Resume Analyzer Agent
**Stack:** Python / LangExtract / Ollama (gemma3:4b) | **License:** Open Source
Resume Analyzer Agent is a **fully local, 100% offline** resume analysis tool powered by LangExtract + Ollama with gemma3:4b [citation:12]. It provides **span evidence** (color-coded highlights showing exactly where each field was extracted), skill intelligence (frequency, domain clustering, JD matching with gap analysis), PDF support via pdfplumber, and JSON export. A Streamlit UI with 5 tabs makes it accessible, with demo mode for instant testing [citation:12].  
**Best for:** Privacy-conscious teams wanting **fully offline** extraction with span evidence and skill intelligence, accepting that gemma3:4b requires local Ollama setup and is slower than ONNX-based extractors.

### SmartHire
**Stack:** Python / Flask / spaCy / MongoDB | **License:** Open Source
SmartHire is a web-based application that automates resume screening and ranking using NLP techniques [citation:3]. Features include role-based authentication for applicants and recruiters, resume upload and parsing (contact details, skills, education, experience), job description management, **TF-IDF or BERT + Cosine Similarity** for resume-JD matching, and detailed match insights showing matched skills, missing skills, and match score per applicant. It includes recruiter and applicant dashboards [citation:3].  
**Best for:** Teams wanting a Flask-based reference implementation of resume-JD matching with TF-IDF/BERT and a recruiter dashboard, accepting a MongoDB dependency and lighter production hardening than CandiSift.

### HireFlow
**Stack:** Django REST / React / PostgreSQL / scikit-learn | **License:** Open Source
HireFlow is an AI-powered recruitment platform with **explainable match scores** [citation:13]. It provides a full REST API with versioned endpoints for auth (JWT with rotation), jobs, applications, resume upload, match calculation, and pipeline views. It includes Docker Compose deployment with PostgreSQL 16, a health check endpoint, and production guard rails (refuses to start without a unique `DJANGO_SECRET_KEY`) [citation:13].  
**Best for:** Full-stack teams wanting a Django/React ATS with explainable matching and Docker deployment, accepting a broader platform scope than a pure parser.

### OpenCATS
**Stack:** PHP / MySQL | **License:** GPL-3.0
OpenCATS is a free and open-source **Applicant Tracking System** (ATS) and recruitment CRM for staffing agencies and hiring teams, managing the recruiting process from job posting through candidate selection and submission [citation:7]. It has an active modernization roadmap covering PHP 8.4/8.5 fixes, database and UI improvements, and larger recruitment, search, API, and integration features. **Important distinction:** OpenCATS is an ATS platform rather than a resume parser—parsing would need to be integrated separately.  
**Best for:** Staffing agencies wanting a proven open-source ATS foundation, accepting that resume parsing must be added via integration.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Parsing Accuracy | Local/Offline | Matching | Best For |
|----------|---------|-------|------------------|---------------|----------|----------|
| **Textkernel** | Proprietary | Cloud | Enterprise-grade | ❌ | ✅ Semantic | Enterprise normalization |
| **Affinda** | Proprietary | Cloud/Self-host | 50+ languages | (Self-host) | ✅ | Broad language + self-host |
| **RChilli** | Proprietary | Cloud | 40+ languages | ❌ | ✅ | API-first control |
| **SmartResume** | Open Source | Python/LLM/OCR | 93.1% | ✅ (vLLM) | ❌ | Layout-aware LLM parsing |
| **CandiSift** | Open Source | Python/FastAPI | LLM-based | ✅ (Stub) | ✅ Bias-audited | Privacy-first AI screening |
| **resume-extract** | Open Source | TS/ONNX | 97.77% entity F1 | ✅ 100% local | ❌ | Blazing-fast offline extraction |
| **resume-parser-ats** | Open Source | TS/Node | (ATS scoring) | ✅ 100% local | ❌ | Local ATS grading + MCP |
| **CVInsight** | Open Source | Python/Gemini | LLM-based | ❌ (Cloud LLM) | ❌ | Granular Python extraction |
| **Resume Analyzer** | Open Source | Python/Ollama | LLM-based | ✅ 100% offline | ✅ JD gap | Offline + span evidence |
| **SmartHire** | Open Source | Flask/spaCy | TF-IDF/BERT | ✅ | ✅ | Reference implementation |
| **HireFlow** | Open Source | Django/React | Explainable | ✅ | ✅ | Full-stack ATS + Docker |
| **OpenCATS** | GPL-3.0 | PHP/MySQL | (No parser) | ✅ | ❌ | Open-source ATS foundation |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Resume Parsing or Candidate Screening tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem **splits** between **high-accuracy layout-aware LLM parsers** (SmartResume from Alibaba with 93.1% extraction accuracy [citation:1]), **privacy-first AI screening platforms** (CandiSift with PII stripping and bias auditing [citation:2]), **blazing-fast local ONNX extractors** (resume-extract at ~15ms per resume with 97.77% entity F1 [citation:11]), **local ATS scoring tools** (resume-parser-ats with MCP integration [citation:5]), and **full ATS platforms** (HireFlow, OpenCATS). No single open-source project replicates the full enterprise breadth of Textkernel or Affinda (50+ languages, taxonomy normalization, self-hosting), but SmartResume and CandiSift cover the most demanding parsing and screening use cases respectively.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
