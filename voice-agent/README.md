# Voice Agent — Autonomous AI Calling System

> Handles all inbound calls from the company website contact page — qualifies leads, answers candidate queries, schedules interviews, and sends confirmations automatically.

![Twilio](https://img.shields.io/badge/Twilio-Voice-red)
![ElevenLabs](https://img.shields.io/badge/ElevenLabs-Voice%20AI-black)
![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)
![Status](https://img.shields.io/badge/Status-Production-brightgreen)

---

## Overview

The Voice Agent is a fully autonomous AI calling system that handles every inbound call from the company's "Contact Us" page without any human operator involvement. It identifies who is calling, adapts its conversation accordingly, and takes the appropriate action — whether that's explaining services, discussing job openings, or booking a meeting.

No call goes unanswered. No follow-up is forgotten.

---

## Problem Solved

Handling inbound calls from a website contact page requires someone available at all times to:
- Qualify whether the caller is a client, a job candidate, or a general inquiry
- Explain services or job openings accurately and consistently
- Schedule meetings without checking calendars manually
- Send confirmation details after every call

This system handles all of that autonomously, 24/7.

---

## System Architecture

```
Incoming Call (Twilio)
        ↓
    Voice AI (ElevenLabs)
    Greets caller, asks purpose of call
        ↓
    Gemini LLM
    Classifies caller intent
        ↓
┌─────────────────────────────┐
│                             │
│  Path A          Path B     │
│  Client Inquiry  Candidate  │
│                             │
│  Explain         Check      │
│  Services        Openings   │
│  + Pricing       + Process  │
│  Context         Details    │
│                             │
└──────────┬──────────┬───────┘
           ↓          ↓
    Schedule Meeting / Interview
           ↓
    Google Calendar → Create Event
           ↓
    Generate Google Meet Link
           ↓
    Send WhatsApp Confirmation
    Send Personalized Email
           ↓
    Log to MySQL Database
```

---

## Call Flows

### Path A — Client Inquiry
Caller is a potential client asking about services.
- Voice agent explains company services based on Pinecone knowledge base
- Answers specific questions about capabilities, pricing context, and process
- Offers to schedule a discovery call
- Books appointment in Google Calendar
- Sends Google Meet link + personalized email + WhatsApp message

### Path B — Job Candidate / Intern
Caller is interested in joining the company.
- Agent explains company background, culture, and tech stack
- Checks current openings from internal database
- Explains selection process step by step
- Offers to schedule an interview or intro call
- Books slot, sends Google Meet link and confirmation via email and WhatsApp

---

## Features

- **24/7 availability** — handles calls outside business hours
- **Human-like voice** — ElevenLabs custom-trained voice model
- **Context-aware responses** — Pinecone RAG for accurate, up-to-date answers
- **Calendar integration** — real-time availability check before booking
- **Multi-channel confirmation** — Google Meet link sent via both email and WhatsApp
- **Full call logging** — every interaction stored in MySQL with timestamp and outcome

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Phone Number + Call Handling | Twilio |
| Voice Synthesis | ElevenLabs (custom voice model) |
| LLM / Conversation Logic | Google Gemini |
| Vector Store (RAG) | Pinecone |
| Workflow Orchestration | n8n |
| Calendar Integration | Google Calendar API |
| Email | Gmail API |
| Messaging | WhatsApp Business API |
| Database | MySQL |

---

## AI Components

- **Intent Classification** — Gemini identifies caller type (client vs candidate) from opening responses
- **RAG Retrieval** — Pinecone queried for accurate company-specific answers
- **Dynamic Conversation** — system prompt adapts based on caller path
- **Confirmation Generation** — personalized email and WhatsApp message generated per caller

---

## Security Considerations

- No sensitive company data spoken over call — answers scoped to knowledge base
- All call recordings and logs stored in secured MySQL instance
- Calendar access uses scoped OAuth token — read/write appointments only
- Twilio webhook validated with signature verification

---

## Results

- Eliminated 100% of manual inbound call handling for routine inquiries
- Every caller receives consistent, accurate information regardless of time of day
- Appointment confirmation sent within seconds of call ending
- Zero missed follow-ups — all bookings logged and tracked

<!-- ## Demo -->

<!-- Add call flow diagram here -->
<!-- Add screenshot of n8n workflow here -->
<!-- Add demo video link here -->

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `TWILIO_ACCOUNT_SID` | Twilio account SID |
| `TWILIO_AUTH_TOKEN` | Twilio auth token |
| `TWILIO_PHONE_NUMBER` | Twilio phone number |
| `ELEVENLABS_API_KEY` | ElevenLabs API key |
| `ELEVENLABS_VOICE_ID` | Custom voice model ID |
| `GEMINI_API_KEY` | Google Gemini API key |
| `PINECONE_API_KEY` | Pinecone key |
| `GOOGLE_CALENDAR_TOKEN` | Google Calendar OAuth token |
| `GMAIL_TOKEN` | Gmail OAuth token |
| `WHATSAPP_API_KEY` | WhatsApp Business API key |

---

## Future Improvements

- Add sentiment detection to escalate frustrated callers to human agent
- Support multilingual calls (Hindi + English)
- Add post-call satisfaction survey via WhatsApp

---

> **Note:** Source code and workflow JSON contain internal configurations. Full system walkthrough available during interview process.
