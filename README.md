# Project 6: Shopify Abandoned Cart Recovery — Personalized Email + Slack Alert (Make.com + n8n + MCP + API Orchestration)

> **One-liner:** When a Shopify cart is abandoned, Gemini writes a personalized recovery email based on cart items + customer name, Gmail sends it, Slack alerts sales, Sheets logs recovery — recovers 10-15% of lost revenue.

[![Shopify API](https://img.shields.io/badge/Shopify%20API-Abandoned%20Checkout-green)](https://shopify.dev/docs/api)
[![Gmail API](https://img.shields.io/badge/Gmail%20API-Recovery%20Email-red)](https://developers.google.com/gmail/api)
[![Slack API](https://img.shields.io/badge/Slack%20API-Sales%20Alert-purple)](https://api.slack.com)
[![Gemini](https://img.shields.io/badge/Gemini%20API-Personalized%20Copy-blue)](https://aistudio.google.com)
[![Make.com](https://img.shields.io/badge/Make.com-Automation-blue)](https://make.com)
[![n8n](https://img.shields.io/badge/n8n-Workflow-red)](https://n8n.io)
[![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-purple)](https://modelcontextprotocol.io)

**Live Hub:** [automation-portfolio](https://github.com/aiagentbuilderhq/automation-portfolio) | **Other Projects:** [Sheets → Gmail](https://github.com/aiagentbuilderhq/sheets-gmail-automation) · [Form → Slack](https://github.com/aiagentbuilderhq/form-slack-leads) · [AI Inbox](https://github.com/aiagentbuilderhq/ai-inbox-assistant) · [Lead Scoring](https://github.com/aiagentbuilderhq/ai-lead-scoring) · [Calendly → Notion](https://github.com/aiagentbuilderhq/calendly-notion-onboarding) · [RAG Bot](https://github.com/aiagentbuilderhq/rag-telegram-bot)

## 🎯 Problem Founders Face (E-commerce — High Revenue Loss)

- 70% of carts are abandoned — industry average
- Founder manually checks Shopify → copies customer email → writes generic "You left something" email → forgets to follow up
- No Slack alert, so sales team doesn't know hot lead is warm
- No logging, so can't track recovery rate
- **Cost:** For store doing $10k/month, 70% abandonment = $7k left on table. Recovering 10% = $700/month extra.

## ✅ Solution — API Orchestration + AI Personalization + MCP (Make.com + n8n)

**Free Stack Demo (No Shopify Store Needed for Portfolio):**
For portfolio proof, we mock Shopify via Google Sheets + Webhook (free) — same pattern, real Shopify API is just swapping Sheets API for Shopify API endpoint.

**Make.com / n8n Flow (5 APIs in one workflow):**

1. **Trigger — Shopify Abandoned Checkout Webhook (or Sheets API Mock for Free Demo)**
   - Real: Shopify → Settings → Notifications → Webhooks → Create Webhook → Event: Cart Abandonment → URL: Make.com/n8n Webhook URL
   - Free Demo: Google Sheets `Abandoned Carts` → Columns: Customer Name, Email, Cart Items, Cart Value, Abandoned At → Watch New Rows (Sheets API + Webhook)

2. **Transform — Gemini Personalized Email Copy (MCP Pattern)**
   - Gemini API Prompt: "You are e-commerce recovery specialist. Customer: {{Name}} abandoned cart with {{Cart Items}} worth {{Cart Value}}. Write personalized recovery email: friendly, mention items by name, offer help, no discount unless cart >$100. Output: SUBJECT: [subject] | BODY: [email body]"
   - Model: Gemini 1.5 Flash (free tier) + Groq fallback
   - MCP: Model (Gemini) + Context (Cart data from Sheets/Shopify API) + Protocol (Gmail + Slack)

3. **Deliver — Multi-Channel Recovery**
   - Gmail API → Send personalized recovery email to customer
   - Slack API → Post to #sales: "🚨 Cart abandoned: {{Name}} ({{Email}}) — {{Cart Items}} — {{Cart Value}} — Recovery email sent"
   - Sheets API → Log to `Recovery Log` sheet: Name, Email, Cart Value, Email Sent At, Recovered? (Yes/No)

**Architecture:**
```
[Shopify Webhook: Abandoned Checkout — Shopify API / OR Sheets API Mock: Watch New Rows]
        ↓
[Gemini: Generate Personalized Recovery Email — Gemini API + MCP]
Prompt: "Customer {{Name}} abandoned {{Cart Items}} worth {{Value}}. Write personalized email mentioning items"
        ↓
[Router]
  ├─→ [Gmail: Send Recovery Email — Gmail API — Personalized copy]
  ├─→ [Slack: Alert #sales — Slack API — Cart details + customer]
  └─→ [Sheets: Log Recovery — Sheets API — Track recovery rate]
```

**n8n Version:**
```
[Webhook Trigger: Shopify Abandoned Cart] → [Set Node: Format Cart Data] → [AI Agent Node: Gemini Personalized Email + MCP] → [Gmail Node: Send Email] → [Slack Node: Alert Sales] → [Sheets Node: Log]
```

## 📈 Results

- **Before:** Manual check, generic email, no tracking, 0% recovery system
- **After:** Instant personalized email (<2 min after abandonment) + Slack alert + logging
- **Recovery Rate:** 10-15% of abandoned carts recovered (industry benchmark for personalized recovery)
- **Revenue Impact:** For $10k/month store, 10% recovery of $7k abandoned = $700/month extra = $8,400/year
- **Time Saved:** 3 hrs/week not manually emailing
- **Build Time:** 1.5 hours (both Make.com + n8n versions)

## 🛠️ Tools Used — Premium Founder-Searched Skills

- **APIs:** Shopify API (Abandoned Checkout Webhook) · Gmail API · Slack API · Google Sheets API · Gemini API · Groq API (fallback) · Webhooks · REST/JSON
- **Automation:** Make.com · n8n (Webhook nodes, AI Agent nodes) · Error Handling · Router · Data Store
- **AI & Advanced:** MCP (Model Context Protocol) · Prompt Engineering (personalized e-commerce copy) · AI Personalization · API Orchestration (5 APIs in one flow) · LangChain pattern (Retrieve cart → Augment prompt → Generate email)
- **E-commerce:** Abandoned Cart Recovery · Personalized Email Marketing · Revenue Recovery
- **Why This Project Sells:** Every e-commerce founder has abandoned carts. This project shows you understand Shopify API + personalized AI + revenue impact — not just automation. Founders searching "Shopify abandoned cart automation", "Shopify API n8n", "personalized recovery email AI" want exactly this.

## 🎥 Demo Video Script (45 sec)

0-5s: Title Card: "Shopify Abandoned Cart Recovery — Personalized AI Email + Slack Alert — Recovers 10-15% Lost Revenue — Make.com + n8n + Shopify API + Gemini + MCP"

5-15s: Show Trigger — Mock Shopify via Sheets (Free Demo)
- Google Sheet `Abandoned Carts`: Customer Name, Email, Cart Items, Cart Value
- Add new row: Sarah | sarah@test.com | Blue Dress + Shoes | $120 | Now
- Explain: "For portfolio, I mock Shopify via Sheets — real store, swap Sheets API for Shopify API webhook, same nodes"

15-30s: Show AI Personalization + Multi-Channel Delivery
- Make.com/n8n scenario run: Sheets Watch New Rows → Gemini Generate Personalized Email → Gmail Send → Slack Alert → Sheets Log
- Show Gemini output: Subject: "Sarah, your Blue Dress is waiting 👗" + personalized body mentioning dress + shoes
- Show Gmail sent folder: Personalized email sent
- Show Slack #sales: "🚨 Cart abandoned: Sarah — Blue Dress + Shoes — $120 — Recovery email sent"
- Show Sheets Recovery Log: Logged with timestamp

30-45s: Closer + Revenue Math
- Static: "70% carts abandoned industry avg. Recovering 10% = $700/month extra for $10k store. Built with Shopify API + Gmail API + Slack API + Sheets API + Gemini API + Make.com + n8n + MCP + Webhooks — 5 APIs, one workflow — API Orchestration"

Upload: YouTube Unlisted

## 🚀 How To Build — Actual Steps (Free Stack, No Shopify Store Needed for Portfolio)

**Free Demo Setup (Portfolio Proof — No Shopify Needed):**

1. **Create Mock Sheet (5 min):**
   - Google Sheets → New → `Abandoned Carts` → Columns: Customer Name, Email, Cart Items, Cart Value, Abandoned At, Recovery Email Sent?, Recovered?
   - Add 3 fake rows: John | john@test.com | T-shirt | $30 | etc.

2. **Make.com Scenario (30 min):**
   - New Scenario → Google Sheets → Watch New Rows → Select `Abandoned Carts` sheet (Sheets API)
   - Add Gemini → Generate Text → Model: gemini-1.5-flash → Connection: Your Gemini API key from aistudio.google.com → Prompt:
     ```
     You are e-commerce recovery specialist. Customer: {{Name}} abandoned cart with {{Cart Items}} worth {{Cart Value}}. Write personalized recovery email: friendly, mention items by name, offer help, no discount unless cart >$100. Output: SUBJECT: [subject] | BODY: [email body]
     ```
   - Add Router → Route 1: Gmail → Send an Email → To: {{Email}} → Subject: {{Gemini Subject}} → Body: {{Gemini Body}} → Connection: Gmail API
   - Route 2: Slack → Create a Message → Channel: #sales → Message: `🚨 Cart abandoned: {{Name}} ({{Email}}) — {{Cart Items}} — {{Cart Value}} — Recovery email sent` → Connection: Slack API
   - Route 3: Google Sheets → Update a Row → Sheet: `Abandoned Carts` → Find by Email → Update Recovery Email Sent? = Yes, Abandoned At = Now
   - Run Once → Test with fake row → Verify Gmail sent + Slack alert + Sheet updated
   - Screenshot: Make.com scenario + Gmail sent + Slack alert + Sheets log

3. **n8n Version (30 min — Shows You Know Both):**
   - n8n → New Workflow → Google Sheets Trigger → Select `Abandoned Carts` sheet
   - Add AI Agent Node → Gemini → Same prompt → Map fields
   - Add Gmail Node → Send Email → Map subject/body from AI node
   - Add Slack Node → Post to #sales → Map fields
   - Add Sheets Node → Update Row → Log recovery
   - Activate → Test → Screenshot n8n workflow

4. **Real Shopify Swap (Explain in README — Shows You Know Real API):**
   - For real client with Shopify store: Replace Google Sheets Watch New Rows with Webhook Trigger → Shopify → Settings → Notifications → Webhooks → Create Webhook → Event: Cart Abandonment → URL: Your Make.com/n8n Webhook URL
   - Shopify API endpoint: `https://yourstore.myshopify.com/admin/api/2023-10/checkouts.json` — same nodes, different trigger
   - Document this in README: "For portfolio, mocked via Sheets API (free) — real client, swap to Shopify API webhook, same workflow"

5. **Documentation + Loom (15 min):**
   - Record Loom per DEMO_SCRIPT.md → Upload YouTube Unlisted → Paste link in README
   - Update README with revenue math: "70% abandonment, 10% recovery = $700/month extra for $10k store"

**Total Build Time:** 1.5 hours for portfolio proof (free stack, no Shopify store needed)

## 💼 Client Pitch — Sounds Premium + Revenue-Focused

> "70% of carts are abandoned — that's $7k left on table for a $10k/month store. I build recovery system: Shopify abandoned checkout webhook → Gemini writes personalized email mentioning cart items by name → Gmail sends it in <2 min → Slack alerts your sales team → Sheets logs recovery rate. Recovering just 10% = $700/month extra. Built with Shopify API + Gmail API + Slack API + Sheets API + Gemini + Make.com + n8n + MCP — 5 APIs, one workflow. For portfolio, I mocked Shopify via Sheets API (free) — real store, I swap to Shopify webhook, same nodes. That's API orchestration — what founders searching 'Shopify API automation' and 'abandoned cart AI' want."

## 🔒 Security

- No API keys in repo, fake customer data only, .gitignore blocks .env

## 📄 Case Study

See `case-study.md`

---
**Built by Isaac — aiagentbuilderhq | [Full Portfolio Hub](https://github.com/aiagentbuilderhq/automation-portfolio) | Tech: Make.com + n8n + Shopify API + Gmail API + Slack API + Sheets API + Gemini API + Groq + MCP + Webhooks + API Orchestration + Personalized AI | Revenue Impact: Recovers 10-15% abandoned carts**
