# Lead Discovery Agent & Multi-Agent Outreach Pipeline

An autonomous, enterprise-grade multi-agent lead discovery and cold outreach pipeline built for **Technewity Labs**.

This system automatically discovers, enriches, scores, and exports high-quality B2B leads across 7 search platforms into Google Sheets, and drafts/sends personalized outreach emails directly from **`contact@technewity.com`**.

---

## 🌟 Key Features

- 🔍 **7 Multi-Source Lead Scraping**: Discovers prospects across Google Maps, Serper Web, Reddit, LinkedIn, Instagram, Facebook, and X/Twitter.
- ✉️ **Email Enrichment**: Integrates with Hunter.io API for verified professional emails.
- 🧠 **Dual-Agent Architecture**:
  - **AI Agent #1 (Query Planner)**: Formulates targeted search queries based on Ideal Customer Profile (ICP) criteria.
  - **AI Agent #2 (Scoring Agent)**: Evaluates leads against ICP using Groq `llama-3.3-70b-versatile` (0-100 score + match explanation).
- 📊 **Google Sheets Integration**:
  - Automatically appends deduplicated qualified leads into target Google Sheets (`Sheet1`).
  - Logs run execution statistics (`Run Log`).
- 📧 **Automated Outreach**: Drafts and sends personalized cold emails using official account `contact@technewity.com`.
- 🔒 **Built-in Safety Toggle**: Dry-run test mode enabled by default to review drafted emails before sending.

---

## 📂 Included Workflows

1. **`lead_discovery_workflow.json`**: Primary discovery, scoring, and sheet export workflow.
2. **`LinkedIn Outreach Agent.json`**: Automated email drafting, status tracking, and outreach sub-workflow.
3. **`linkedin_outreach_dashboard.html`**: Interactive HTML dashboard for lead tracking.

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- [n8n Self-Hosted](https://n8n.io/) (`n8n >= 2.29.10`)
- Google Cloud Project with Google Sheets & Gmail APIs enabled
- API Keys: Groq, Serper.dev, Hunter.io, Apify

### 2. Environment Configuration
Create a `.env` file in the root directory (never commit to Git):

```env
GROK_API_KEY=gsk_your_groq_api_key
SERPER_API_KEY=your_serper_dev_key
HUNTER_API_KEY=your_hunter_io_key
N8N_GOOGLE_CLIENT_ID=your_google_client_id
N8N_GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_SHEET_ID=your_google_sheet_id
```

### 3. Import Workflows into n8n
1. Open n8n UI at `http://localhost:5678`.
2. Go to **Workflows** -> **Import from File** -> Select `lead_discovery_workflow.json` and `LinkedIn Outreach Agent.json`.
3. Link your API credentials in n8n (Groq, Serper, Hunter.io, Google Sheets, Gmail).
4. Activate both workflows!

### 4. Running Lead Discovery
1. Click **Test workflow** on `Lead Discovery Agent`.
2. The form trigger comes prefilled with **Technewity Labs** defaults:
   - Target Geography: `India`
   - Offerings: Website Development, AI Solutions & Agents, Business Process Automation
3. Click **Submit** to run the complete pipeline!

---

## 🛡️ Safety & Dry-Run Mode
The outreach sending nodes (`Send Outreach Email` & `Send LinkedIn Message`) are set to **Disabled** by default. All drafted emails are logged to Google Sheets so you can review them before enabling live message delivery.

---

## 📄 License
Privately developed for **Technewity Labs**.
