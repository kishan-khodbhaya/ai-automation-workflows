# Blog Writer — AI-Powered Content Pipeline with Human Approval

> End-to-end blog creation system: topic input via Telegram → AI drafting → owner review and feedback → revision → auto-publish to Blogspot.

![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)
![Gemini](https://img.shields.io/badge/Gemini-LLM-blue)
![Telegram](https://img.shields.io/badge/Telegram-Interface-blue)
![Status](https://img.shields.io/badge/Status-Production-brightgreen)

---

## Overview

The Blog Writer is a fully automated content pipeline that takes a topic from a Telegram message and produces a complete, SEO-optimized blog post — including research, section drafts, human-like rewriting, image generation, and a thumbnail — all approved and revised by the owner through Telegram before being saved to Google Docs and scheduled for publishing.

The owner stays in control at every step. The system does the work.

---

## Problem Solved

Publishing consistent, high-quality blog content requires significant manual effort:
- Research for each topic
- Writing multiple sections coherently
- Generating and selecting images
- SEO optimization
- Formatting and publishing

This pipeline automates every step while keeping the owner in the loop for approval and feedback — so content quality stays high without the time investment.

---

## System Architecture

```
Owner sends topic via Telegram
        ↓
    n8n receives message
        ↓
    Research Phase
    BraveSearch + SerpAPI gather context
        ↓
    Drafting Phase (per section)
    ┌─────────────────────────────────┐
    │  Header drafted individually    │
    │  Main Section 1 drafted         │
    │  Main Section 2 drafted         │
    │  Footer drafted                 │
    └─────────────────────────────────┘
        ↓
    Humanization Pass
    Gemini rewrites to remove AI tone
        ↓
    Image Generation
    Blog images + thumbnail generated
        ↓
    Owner Review via Telegram
    Full draft + images sent for approval
        ↓
┌─────────────────┐    ┌──────────────────────┐
│   Approved       │    │  Feedback Received    │
│        ↓         │    │  Owner specifies what │
│  Save to         │    │  to change (text or   │
│  Google Docs     │    │  image)               │
│        ↓         │    │        ↓              │
│  Owner schedules │    │  System revises only  │
│  publish date    │    │  that section/image   │
│        ↓         │    │        ↓              │
│  Auto-publish    │    │  Re-sent for approval │
│  via Blogspot API│    └──────────────────────┘
└─────────────────┘
```

---

## Features

- **Section-by-section drafting** — header, main sections, and footer drafted independently for better quality control
- **Humanization layer** — separate Gemini pass removes AI writing patterns before review
- **Image generation** — blog body images and thumbnail generated automatically
- **Telegram-based approval** — owner reviews and approves or gives specific feedback in chat
- **Partial revision** — only the specific section or image the owner flags gets re-drafted, not the whole blog
- **Google Docs storage** — approved content saved in structured Google Doc
- **Scheduled publishing** — owner sets publish date, system handles Blogspot API publish

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Workflow Orchestration | n8n |
| LLM (Drafting + Humanizing) | Google Gemini |
| Research | Brave Search API, SerpAPI |
| Owner Interface | Telegram Bot API |
| Image Generation | Gemini Image Generation |
| Document Storage | Google Docs API |
| Publishing | Blogspot API |

---

## AI Components

- **Research agent** — queries Brave Search and SerpAPI for current, relevant information per topic
- **Section drafting** — each section uses a tailored system prompt for better structure and depth
- **Humanization pass** — dedicated Gemini prompt that rewrites content to sound natural
- **Feedback routing** — Gemini classifies owner feedback as text revision or image revision and routes accordingly

---

## Workflow Design Decision

Each blog section (header, main 1, main 2, footer) is drafted by a separate AI node with its own system prompt. This produces significantly better output than prompting for an entire blog at once — each section gets focused attention and the right tone for its purpose.

---

## Results

- Reduced blog production time from several hours to owner review time only
- Consistent publishing cadence maintained without manual writing effort
- Owner retains full editorial control through the Telegram approval flow


<!-- ## Demo -->

<!-- Add Telegram conversation screenshot here -->
<!-- Add workflow diagram here -->
<!-- Add sample blog output screenshot here -->
<!-- Add demo video link here -->

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `GEMINI_API_KEY` | Google Gemini API key |
| `BRAVE_SEARCH_API_KEY` | Brave Search API key |
| `SERP_API_KEY` | SerpAPI key |
| `TELEGRAM_BOT_TOKEN` | Telegram bot token |
| `TELEGRAM_OWNER_CHAT_ID` | Owner's Telegram chat ID |
| `GOOGLE_DOCS_TOKEN` | Google Docs OAuth token |
| `BLOGSPOT_API_KEY` | Blogspot API key |
| `BLOGSPOT_BLOG_ID` | Target blog ID |

---

## Future Improvements

- Add WordPress publishing support alongside Blogspot
- Auto-generate social media posts from approved blog content
- Add SEO score check before sending for approval

---

> **Note:** Workflow JSON available. Contains API configurations specific to deployment. Full walkthrough available during interview process.
