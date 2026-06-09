# AI Email Classification and Routing System

An n8n workflow that uses Groq (LLaMA 3) to automatically read, classify, and route inbound emails — eliminating manual email triage for small businesses.

---

## The Problem

Small business owners waste significant time every day manually reading and sorting inbound emails. Enquiries, complaints, and booking requests all land in the same inbox — and the wrong ones get missed or delayed.

Manual triage is slow, inconsistent, and unscalable.

---

## The Solution

This workflow receives inbound emails via webhook, uses Groq's LLaMA 3 model to classify each email into one of four categories, then automatically routes it to the correct Google Sheet tab and sends a categorised Telegram alert to the business owner.

No manual reading required. Every email is sorted and logged instantly.

---

## How It Works

1. **Email received** — inbound email data posted to a webhook (sender name, email, subject, body)
2. **AI classification** — Groq (LLaMA 3) reads the subject and body, returns a category and one-sentence summary
3. **Parse and normalise** — response is parsed, category validated, original email data merged
4. **Route by category** — Switch node directs flow to the correct branch
5. **Log to Google Sheets** — row appended to the matching tab (Enquiries / Complaints / Booking Requests / Other)
6. **Telegram alert** — owner notified with category emoji, sender details, and AI summary

---

## Categories

| Category | Emoji | Description |
|----------|-------|-------------|
| `enquiry` | 📋 | General questions about services or pricing |
| `complaint` | 🚨 | Negative feedback or issues raised |
| `booking_request` | 📅 | Requests to book an appointment or job |
| `other` | 📌 | Anything that doesn't fit the above |

---

## Stack

| Tool | Role |
|------|------|
| n8n (self-hosted) | Workflow orchestration |
| Groq (LLaMA 3) | AI email classification |
| Google Sheets | Categorised email logging |
| Telegram | Owner alerts |

---

## Use Case

- Instantly classifies inbound emails with no manual reading
- Logs every email to the correct sheet tab with AI-generated summary
- Owner receives real-time Telegram alert with category and context
- Designed for UK hair salons, independent restaurants, and sole-trader trades

---

## Setup

### Prerequisites
- n8n instance (self-hosted or cloud)
- Groq API key (free tier works)
- Google Sheets with service account or OAuth credentials
- Telegram bot token
- Google Sheet with four tabs: `Enquiries`, `Complaints`, `Booking Requests`, `Other`

Each tab needs these columns: `Timestamp`, `Sender Name`, `Sender Email`, `Subject`, `Summary`, `Category`

### Installation

1. Clone or download this repo
2. Import `workflow/email-classifier.json` into your n8n instance
3. Copy `.env.example` to `.env` and fill in your credentials
4. In n8n, create a Header Auth credential: name `Groq API Key`, header `Authorization`, value `Bearer YOUR_GROQ_API_KEY`
5. Connect your Google Sheets and Telegram credentials
6. Set your Google Sheet ID in each Sheets node
7. Set your Telegram Chat ID in each Telegram node
8. Activate the workflow

See `.env.example` for all required environment variables.

---

## Project Status

✅ Built and tested
🧪 Demonstration build — fully functional, available to deploy
📍 Designed for UK small business use cases

---

## Author

**Zayd Akhtar** — AI Automation Builder
[LinkedIn](https://www.linkedin.com/in/zayd-a-03b681144/) · [GitHub](https://github.com/zaydakhtar)
Open to remote contracts and consulting · Based in the UK
