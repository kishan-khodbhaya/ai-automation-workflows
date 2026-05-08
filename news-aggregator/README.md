# News Aggregator — AI-Powered PDF News Extraction

> Extracts targeted keywords, job openings, and advertisements from newspaper PDF scans and delivers structured summaries via Telegram.

![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)
![Gemini](https://img.shields.io/badge/Gemini-LLM-blue)
![Telegram](https://img.shields.io/badge/Telegram-Output-blue)
![Status](https://img.shields.io/badge/Status-Production-brightgreen)

---

## Overview

The News Aggregator processes physical newspaper PDFs — including scanned images of print editions — and extracts specific information: job openings, advertisements, and keyword-matched content. Results are delivered as structured summaries via Telegram, eliminating the need to manually read through entire newspaper editions.

---

## Problem Solved

Monitoring newspapers for relevant job postings, tenders, advertisements, or keyword mentions requires reading through large PDF files manually — time-consuming and easy to miss important entries.

This system automates that monitoring and delivers only the relevant extracted content.

---

## System Architecture

```
Newspaper PDF uploaded / received
        ↓
    n8n receives file
        ↓
    Gemini Vision AI
    Reads PDF pages (including scanned images)
        ↓
    Extraction Engine
    Searches for:
    - Configured keywords
    - Job openings / recruitment ads
    - Tender notices
    - General advertisements
        ↓
    Structured summary generated
        ↓
    Delivered via Telegram message
```

---

## Features

- **Scanned PDF support** — Gemini Vision reads image-based newspaper scans, not just digital PDFs
- **Configurable keywords** — target terms updated without changing the workflow
- **Structured output** — results delivered as clean, readable Telegram messages
- **Multi-category extraction** — jobs, ads, tenders, and custom keywords in one pass
- **On-demand processing** — trigger by sending PDF to the workflow

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Workflow Orchestration | n8n |
| Document Analysis | Google Gemini Vision AI |
| Output Delivery | Telegram Bot API |

---

## Results

- Eliminated manual newspaper scanning for relevant content
- Relevant information extracted and delivered in seconds after PDF input

<!-- ## Demo -->

<!-- Add sample Telegram output screenshot here -->
<!-- Add workflow screenshot here -->

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `GEMINI_API_KEY` | Google Gemini API key |
| `TELEGRAM_BOT_TOKEN` | Telegram bot token |
| `TELEGRAM_CHAT_ID` | Target Telegram chat ID |

---

> **Note:** Workflow JSON available. Full walkthrough available during interview process.
