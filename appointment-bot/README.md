# Appointment Bot — WhatsApp-Based AI Scheduling System

> Same intelligence as the Voice Agent — entirely through WhatsApp messages. No calls, no voice, no manual intervention.

![WhatsApp](https://img.shields.io/badge/WhatsApp-Messaging-brightgreen)
![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)
![Gemini](https://img.shields.io/badge/Gemini-LLM-blue)
![Status](https://img.shields.io/badge/Status-Production-brightgreen)

---

## Overview

The Appointment Bot handles the same workflows as the Voice Agent — client qualification, candidate screening, and appointment scheduling — but entirely through WhatsApp messages. Users who prefer text over calls get the same seamless experience: intelligent responses, real-time calendar checks, and instant confirmations.

---

## Problem Solved

Many users prefer WhatsApp over phone calls, especially for initial inquiries. Without automation, every WhatsApp message requires a human to read, respond, check availability, and send a meeting link — a slow, manual process that doesn't scale.

This system handles the entire conversation autonomously from first message to confirmed booking.

---

## System Architecture

```
Incoming WhatsApp Message
        ↓
    n8n Webhook Receiver
        ↓
    Gemini LLM
    Classifies message intent
        ↓
┌──────────────────────────────┐
│                              │
│  Client Inquiry              │
│  → Service explanation       │
│  → Discovery call booking    │
│                              │
│  Candidate Inquiry           │
│  → Opening status check      │
│  → Process explanation       │
│  → Interview scheduling      │
│                              │
└──────────────┬───────────────┘
               ↓
    Check Google Calendar availability
               ↓
    Book appointment
               ↓
    Generate Google Meet link
               ↓
    Send WhatsApp confirmation + Meet link
               ↓
    Log to MySQL
```

---

## Features

- **Full conversation handling** — multi-turn WhatsApp conversation managed by Gemini
- **Real-time calendar check** — availability verified before confirming any slot
- **Instant confirmation** — Google Meet link sent in the same conversation thread
- **Context retention** — conversation history maintained per user session
- **Fallback handling** — unclear messages prompt clarifying questions before proceeding
- **Full logging** — every conversation and outcome stored in MySQL

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Messaging Interface | WhatsApp Business API |
| Workflow Orchestration | n8n |
| LLM / Conversation | Google Gemini |
| Calendar Integration | Google Calendar API |
| Database | MySQL |
| Confirmation | WhatsApp (same thread) |

---

## Difference from Voice Agent

| Feature | Voice Agent | Appointment Bot |
|---------|------------|----------------|
| Interface | Phone call | WhatsApp messages |
| Voice synthesis | ElevenLabs | Not needed |
| Response style | Spoken conversation | Text conversation |
| Confirmation | Email + WhatsApp | WhatsApp only |
| Use case | Users who call | Users who message |

Both connect to the same Google Calendar and MySQL backend.

---

## Results

- Handles all WhatsApp inquiries without human involvement
- Appointment confirmations sent within seconds of conversation completion
- Consistent responses regardless of volume or time of day

---

<!-- ## Demo -->

<!-- Add WhatsApp conversation screenshot here -->
<!-- Add n8n workflow screenshot here -->
<!-- Add demo video link here -->

---

## Environment Variables

| Variable | Description |
|----------|-------------|
| `WHATSAPP_API_KEY` | WhatsApp Business API key |
| `WHATSAPP_PHONE_ID` | WhatsApp phone number ID |
| `GEMINI_API_KEY` | Google Gemini API key |
| `GOOGLE_CALENDAR_TOKEN` | Google Calendar OAuth token |
| `DB_HOST` | MySQL host |
| `DB_USER` | MySQL user |
| `DB_PASSWORD` | MySQL password |

---

> **Note:** Workflow JSON contains internal configurations. Available for walkthrough during interview process.
