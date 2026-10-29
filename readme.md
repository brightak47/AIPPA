
Here is a detailed, logical, and production-grade architecture workflow for your AI-powered phishing assistant. Designed specifically to be dropped directly into your repository’s `README.md` file, this structured blueprint outlines the system design, components, and data flows required to build and operate a secure, authorized simulation platform.

---

# Project Architecture: AI-Powered Phishing Assistant

## 1. Executive Summary

The AI-Powered Phishing Assistant is an automated security-awareness engineering platform designed to help red teams and security operations centers (SOCs) generate context-aware, highly personalized, and legally compliant phishing simulation campaigns. By leveraging Large Language Models (LLMs) integrated with Open Source Intelligence (OSINT) data pipelines, the tool minimizes manual template creation overhead while accurately simulating advanced threat actor tactics.

---

## 2. High-Level System Workflow

The assistant operates on a closed-loop pipeline consisting of four major phases: **Reconnaissance & Context Ingestion**, **AI Generation & Guardrails**, **Campaign Orchestration & Delivery**, and **Telemetry & Feedback Analysis**.

```
[Target Data / OSINT] ──► [Context Preprocessor] ──► [LLM Generator Engine]
                                                              │
[Analytics Dashboard] ◄── [Tracking & Telemetry] ◄── [Delivery Engine (SMTP)]

```

---

## 3. Detailed Component Breakdown & Workflow

### Phase 1: Reconnaissance and Target Profiling (Context Ingestion)

Before any text is generated, the assistant ingests localized context parameters to ensure high campaign relevance without crossing ethical or unauthorized boundaries.

* **Input Parameters:** Target role/department, seniority level, industry sector, known active company projects (from internal directory feeds or approved public data), and target psychological vectors (e.g., urgency, authority, helpfulness).
* **Data Structuring:** The input layer normalizes this data into a standardized JSON schema (`CampaignContext`) consumed by the generation engine.

### Phase 2: AI Generation Engine and Safety Guardrails

This phase handles prompt compilation, LLM querying, and safety validation to ensure compliance and prevent policy violations.

* **Dynamic Prompt Templating:** Uses role-prompt engineering combined with Cialdini's principles of persuasion (e.g., social proof, scarcity, authority) to mimic realistic modern spear-phishing syntax.
* **Content Generation:** Queries an authorized LLM backend (e.g., locally hosted open-weight models like Llama-3 or securely vetted API endpoints) to produce:
* Email Subject Line (polymorphic variants to test filter resilience)
* Sender Pretext (display name spoofing simulations, internal domain lookalikes)
* Body Copy (hyper-personalized text referencing real-world workflow cadences)


* **Validation & Safety Guardrails Layer:**
* Automated regex checks to strip accidental PII or restricted vocabulary.
* Schema validation ensuring compliance with corporate simulation governance rules.
* Human-in-the-Loop (HITL) review flag: Routes generated outputs to a security analyst dashboard for manual sign-off before execution.



### Phase 3: Campaign Orchestration and Delivery

Once approved, the campaign is handed over to the simulation delivery infrastructure.

* **Template Customization & Tracking Injection:** Injects unique, cryptographically secure tracking identifiers (`target_id` and `campaign_id`) into links and tracking pixels.
* **Safe Landing Page Integration:** Maps click-through events to benign educational landing pages ("teachable moments") rather than capturing or storing raw credentials.
* **Secure Dispatch:** Interfaces with an isolated SMTP relay configured exclusively for authorized simulation testing with proper DKIM/SPF sign-offs.

### Phase 4: Telemetry, Metrics, and Feedback Loop

The final stage captures user behavior to compute human-risk metrics and optimize future training paths.

* **Event Logging:** Captures lifecycle events:
* `Email Delivered` / `Email Opened`
* `Link Clicked` (Primary failure metric)
* `Credential Submitted` (High-risk interaction)
* `Reported via Phishing Button` (Desired defensive action)


* **Risk Scoring & Reporting:** Updates user risk profiles dynamically and pushes feedback data into security awareness platforms via internal APIs or webhook integrations.

---

## 4. Tech Stack Recommendations

| Layer | Recommended Technology | Purpose |
| --- | --- | --- |
| **Backend API** | Python / FastAPI | High-performance asynchronous execution for API integrations and prompt handling |
| **LLM Core** | LangChain / Instructor (Python) | Structured output parsing and prompt management |
| **Database** | PostgreSQL + SQLAlchemy | Relational storage for campaigns, target demographics, and event logs |
| **Queue / Worker** | Celery + Redis | Asynchronous handling of bulk email dispatch and tracking events |
| **Frontend Dashboard** | React / Tailwind CSS | Analyst portal for reviewing templates, managing targets, and viewing analytics |

---

## 5. Security & Compliance Mandates

* **Strict Authorization:** This tool must *only* be executed against domains, assets, and personnel explicitly covered under a signed Rules of Engagement (RoE) contract or internal authorization policy.
* **Credential Handling:** Under no circumstances should real user credentials submitted during simulation testing be stored in plaintext. If credential harvesting is simulated, capture only a boolean flag indicating submission status.
* **Data Privacy:** Ensure target metadata complies with regional privacy regulations (e.g., GDPR, CCPA).
