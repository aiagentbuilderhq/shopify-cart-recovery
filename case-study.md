# Case Study: Shopify Abandoned Cart Recovery — Personalized AI Email + Slack + Sheets

**Client Type:** E-commerce store doing $10k/month, 70% cart abandonment
**Timeline:** 1.5 hours
**Tools:** Shopify API (or Sheets mock for free demo), Gmail API, Slack API, Sheets API, Gemini API, Groq, Make.com, n8n, MCP, Webhooks
**Cost to Run:** $0/month free tiers

### Problem
70% carts abandoned industry average. Founder manually checks Shopify, writes generic "You left something" email, forgets follow-up, no Slack alert, no logging. $10k/month store = $7k abandoned/month. No recovery system = $0 recovered.

### Solution
Built 5-API orchestration:
1. Trigger: Shopify Abandoned Checkout Webhook (or Sheets mock for portfolio) — Sheets API Watch New Rows
2. Transform: Gemini generates personalized recovery email mentioning cart items by name — MCP pattern
3. Deliver: Gmail sends personalized email in <2 min + Slack alerts #sales + Sheets logs recovery rate

**Flow:** Abandoned Cart (Shopify API / Sheets API) → Gemini Personalized Email (Gemini API + MCP) → Gmail Recovery Email (Gmail API) + Slack Alert (Slack API) + Sheets Log (Sheets API)

### Results
- Recovery Rate: 10-15% of abandoned carts (industry benchmark for personalized)
- Revenue: For $10k/month store, 10% of $7k abandoned = $700/month extra = $8,400/year
- Time Saved: 3 hrs/week not manually emailing
- Personalization: Email mentions items by name — feels human, not generic

### What Client Gets
- Working scenario + n8n workflow + blueprint.json (sanitized)
- Loom walkthrough (5 min): how it works, how to edit email copy, how to add discount logic, how to change Slack channel
- Documentation: How to swap Sheets mock to real Shopify webhook, how to adjust prompt for different products
- 7 days support

### Tools & Cost
- Shopify API (free for store owner), Gmail API free, Slack API free, Sheets API free, Gemini free tier (15 req/min), Make.com free (1,000 ops), n8n free self-host
- Running cost $0 — client pays for build + upkeep

### Why Premium
E-commerce founders pay $400-600 for abandoned cart recovery that recovers revenue. Shows you understand Shopify API + personalized AI + revenue math + API orchestration — not just automation.

---
Demo: [Add Link] | Portfolio: github.com/aiagentbuilderhq/automation-portfolio
