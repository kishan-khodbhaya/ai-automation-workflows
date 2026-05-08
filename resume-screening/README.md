# Resume Screening — AI-Powered HR Pipeline

> Accepts resumes via WhatsApp, scores them against role criteria, and triggers the interview pipeline automatically.

![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)
![Gemini](https://img.shields.io/badge/Gemini%20Vision-AI-blue)
![WhatsApp](https://img.shields.io/badge/WhatsApp-Input-brightgreen)
![Status](https://img.shields.io/badge/Status-Production-brightgreen)

---

## Overview

The Resume Screening system automates the first stage of the hiring process. Candidates send their resume as a PDF or image via WhatsApp. The system extracts and analyzes the content using Gemini Vision AI, evaluates it against role criteria, and either triggers the interview scheduling pipeline or sends a rejection notice — with no human involvement in the initial screening step.

---

## Problem Solved

Manual resume screening is time-consuming and inconsistent. Reviewing 20-30 resumes per opening, applying the same criteria each time, and following up with candidates individually takes hours of HR time per hiring cycle.

This system screens every resume instantly, applies consistent criteria, and hands off qualified candidates to the next pipeline stage automatically.

---

## System Architecture

```
Candidate sends resume via WhatsApp
(PDF or image format)
        ↓
    n8n Webhook receives file
        ↓
    File saved to Google Drive
        ↓
    Gemini Vision AI
    Extracts and analyzes resume content
        ↓
    Evaluation Engine
    Scores against role criteria:
    - Skills match
    - Experience level
    - Education requirements
    - Role-specific qualifications
        ↓
┌───────────────────┐    ┌──────────────────────┐
│  Qualified         │    │  Not Qualified        │
│        ↓           │    │        ↓              │
│  Trigger interview │    │  Send polite          │
│  scheduling flow   │    │  rejection via        │
│  (next pipeline)   │    │  WhatsApp + Gmail     │
└───────────────────┘    └──────────────────────┘
```

---

## Features

- **Multi-format input** — accepts both PDF documents and image scans of resumes
- **Vision AI extraction** — Gemini Vision reads and structures resume data even from image files
- **Configurable criteria** — evaluation parameters adjustable per role without changing workflow
- **Dual output** — qualified candidates trigger interview flow, others receive automated response
- **Google Drive archiving** — every resume stored and organized automatically
- **Audit trail** — screening results and decisions logged per candidate

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Input Channel | WhatsApp Business API |
| Workflow Orchestration | n8n |
| Resume Analysis | Google Gemini Vision AI |
| File Storage | Google Drive API |
| Candidate Communication | WhatsApp, Gmail API |

---

## AI Components

- **Gemini Vision** — extracts structured data from both PDF text and image-based resumes
- **Evaluation prompt** — system prompt defines role criteria; Gemini returns structured pass/fail with reasoning
- **Response generation** — personalized rejection or confirmation message generated per candidate

---

## Results

- Screening time reduced from manual review to near-instant automated evaluation
- Consistent criteria applied to every candidate regardless of volume
- Qualified candidates entered the interview pipeline without HR intervention


<!-- ## Demo -->

<!-- Add workflow screenshot here -->
<!-- Add sample screening output here -->
<!-- Add demo video link here -->

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `WHATSAPP_API_KEY` | WhatsApp Business API key |
| `GEMINI_API_KEY` | Google Gemini API key |
| `GOOGLE_DRIVE_TOKEN` | Google Drive OAuth token |
| `GMAIL_TOKEN` | Gmail OAuth token |

---

> **Note:** Workflow JSON available. Full walkthrough available during interview process.
