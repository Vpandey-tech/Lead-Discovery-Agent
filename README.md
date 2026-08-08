# Technewity Labs — Multi-Agent Lead Discovery & Automated Outreach Pipeline

An enterprise-grade, autonomous multi-agent lead discovery and cold outreach system custom-built for **Technewity Labs**.

This system automatically discovers, enriches, scores, and exports high-intent B2B leads across 7 search platforms into Google Sheets, and executes personalized email outreach directly from **`contact@technewity.com`** via the **Resend API**.

---

## 🏗️ Multi-Agent Architecture

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                   STAGE 1: INTAKE & QUERY PLANNING                          │
│  User submits Technewity Labs ICP ➔ Query Planner Agent (AI Agent #1)      │
│  generates intent search queries ("need web dev", "looking for AI agency"). │
└─────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                 STAGE 2: MULTI-PLATFORM INTENT SCRAPING & ENRICHMENT        │
│  Parallel search across Google Maps + Reddit + Web + LinkedIn + IG + FB + X │
│  ➔ Hunter.io API enriches verified corporate emails.                       │
└─────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                 STAGE 3: AI ICP SCORING & DEDUPLICATED STORAGE              │
│  Scoring Agent (AI Agent #2 - Groq llama-3.3-70b) scores fit (0-100)       │
│  ➔ Deduplicates & appends genuine qualified leads into Google Sheets.      │
└─────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                 STAGE 4: AUTOMATED OUTREACH & STATUS TRACKING              │
│  Sub-Workflow Trigger receives qualified lead directly                     │
│  ➔ AI Copywriter drafts personalized email for Technewity Labs            │
│  ➔ Resend API delivers HTML email from contact@technewity.com              │
│  ➔ Updates Sheet Status from 'New' ➔ 'Contacted'.                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 🌟 Key Capabilities

- 🔍 **7 Multi-Source Intent Scraping**: Discovers prospects on Google Maps, Serper Web, Reddit (intent posts), LinkedIn, Instagram, Facebook, and X/Twitter.
- ✉️ **Email Enrichment**: Integrates with Hunter.io API for verified decision-maker emails.
- 🧠 **Dual-Agent AI Engine**:
  - **AI Agent #1 (Query Planner)**: Formulates targeted search queries based on Ideal Customer Profile (ICP).
  - **AI Agent #2 (ICP Scorer)**: Evaluates leads using Groq `llama-3.3-70b-versatile` (0-100 score + match explanation).
- 📊 **Google Sheets Integration**: Appends deduplicated qualified leads to `Sheet1` and logs execution metrics to `Run Log`.
- 📧 **Enterprise Resend Email Delivery**: Delivers styled HTML cold emails directly from **`contact@technewity.com`** via Resend.
- 🔄 **Real-Time Status Synchronization**: Automatically updates lead status from `New` to `Contacted` in Google Sheets upon delivery.

---

## 📂 Included Workflows

1. **`lead_discovery_workflow.json`**: Primary discovery, intent scraping, scoring, and sheet export workflow.
2. **`LinkedIn Outreach Agent.json`**: Automated email drafting, Resend delivery, and sheet status tracking sub-workflow.
3. **`linkedin_outreach_dashboard.html`**: Interactive HTML tracking dashboard.

---

## 📊 Google Sheet Header Structure

Your target Google Sheet (`Sheet1`) contains the following 13 columns:

| Column Header | Description |
| :--- | :--- |
| **Name** | Prospect or Company Name |
| **Title** | Decision Maker Title/Designation |
| **Company** | Target Company Name |
| **Industry** | Business Domain / Niche |
| **Platform** | Scraping Source (Google Maps, Reddit, Web, LinkedIn, etc.) |
| **Profile URL** | Website or Social Profile Link |
| **Email** | Verified Email Address |
| **Location** | City / Region / Country |
| **Score** | ICP Fit Score (0 - 100) |
| **Why Matched** | AI Reasoning for ICP Match |
| **Source** | Sub-system / Scraper Endpoint |
| **Status** | Lead Lifecycle Status (`New` ➔ `Contacted`) |
| **Discovered At** | ISO Timestamp of Lead Discovery |

---

## 🚀 Setup & Execution Guide

### 1. Prerequisites
- [n8n Self-Hosted](https://n8n.io/) (`n8n >= 2.29.10`)
- Google Cloud Project with Google Sheets API enabled
- Resend.com Account with Verified Domain (`technewity.com`)
- API Keys: Groq, Serper.dev, Hunter.io, Apify, Resend

### 2. Environment Configuration
Create a `.env` file in the project root (never commit to Git):

```env
GROK_API_KEY=gsk_your_groq_api_key
SERPER_API_KEY=your_serper_dev_key
HUNTER_API_KEY=your_hunter_io_key
RESEND_API_KEY=re_your_resend_api_key
GOOGLE_SHEET_ID=1vOP6GX4ShQq1f5Msb7HgCuCgGI9M8qkOsPYwcx0P6hI
```

### 3. Resend Credential Setup in n8n
1. Open n8n at `http://localhost:5678/credentials`.
2. Click **Add Credential** -> **Header Auth**.
3. Name: `Header Auth account`
4. Header Name: `Authorization`
5. Header Value: `Bearer re_YOUR_RESEND_API_KEY`
6. Click **Save**.

### 4. Importing & Running Workflows
1. Open n8n UI -> **Workflows** -> **Import from File**.
2. Import `lead_discovery_workflow.json` and `LinkedIn Outreach Agent.json`.
3. Activate both workflows.
4. Click **Test workflow** on `Lead Discovery Agent` to execute the full pipeline!

---

## 🛡️ License & Ownership
Developed exclusively for **Technewity Labs**.
