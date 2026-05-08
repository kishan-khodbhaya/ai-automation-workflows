# ChatOps Engine — Multi-Agent Internal Operations System

> Natural language interface for DevOps, database, server, and knowledge operations — built for internal engineering teams.

![n8n](https://img.shields.io/badge/n8n-Orchestration-orange)
![Gemini](https://img.shields.io/badge/Gemini-LLM-blue)
![Pinecone](https://img.shields.io/badge/Pinecone-RAG-purple)
![Mattermost](https://img.shields.io/badge/Mattermost-Chat-green)
![Status](https://img.shields.io/badge/Status-Production-brightgreen)

---

## Overview

The ChatOps Engine is a multi-agent automation system that allows engineering teams to perform DevOps, database, and infrastructure operations through natural language commands inside Mattermost — without switching tools, writing scripts, or logging into servers manually.

Instead of opening a terminal, writing a query, or searching through documentation — a team member types what they need in chat and the system executes it.

---

## Problem Solved

Engineering teams waste significant time on repetitive operational tasks:
- Manually running database queries to check or fetch data
- Switching between GitHub, Jenkins, and terminal for routine Git and deployment tasks
- Asking colleagues for credentials or internal documentation
- Performing server diagnostics by SSHing into machines

This system centralizes all of these operations into a single chat interface with role-based access control — so the right people can do the right things without the overhead.

---

## System Architecture

```
Mattermost (Chat Interface)
        ↓
    n8n Webhook Receiver
        ↓
    Gemini LLM Router
    (classifies intent → routes to correct agent)
        ↓
┌──────────────────────────────────────────────┐
│                                              │
│  Agent 1       Agent 2       Agent 3         │
│  GitOps        DBOps         DevOps          │
│  (GitHub)      (MySQL)       (Terminal)      │
│                                              │
│  Agent 4       Agent 5                       │
│  Knowledge     Password                      │
│  Base          Vault                         │
│  (Pinecone)    (Encrypted)                   │
│                                              │
└──────────────────────────────────────────────┘
        ↓
    Response formatted + returned to Mattermost
```

---

## Agents

### Agent 1 — GitOps (GitHub Operations)
Handles all Git and code management tasks via chat commands.
- Create and switch branches
- Open, review, and merge pull requests
- Invite team members to repositories
- Check PR status and CI results
- Automated PR link generation and status updates

### Agent 2 — DBOps (Database Operations)
Natural language interface for database queries.
- Run SELECT, INSERT, UPDATE queries via plain English
- Fetch records, check tables, and validate data
- Returns results in clean table or list format
- Secure credential lookup before each operation
- Multi-database support

### Agent 3 — DevOps Terminal (Infrastructure Operations)
System-level operations via chat.
- Server diagnostics — CPU, memory, disk, process status
- Service checks and restarts
- Log fetching and error analysis
- Docker container management
- Deployment triggers via Jenkins

### Agent 4 — Internal Knowledge Base (AI Receptionist)
Company information and documentation assistant.
- Answers questions about services, processes, team, and onboarding
- Powered by Pinecone vector store with embedded internal documents
- Handles client queries about company capabilities
- Escalates sensitive topics to human contacts

### Agent 5 — Password Vault (Credential Management)
Secure internal credential lookup system.
- Retrieve credentials via slash commands
- Hashed + reversible encryption — plaintext never stored
- Role-based access control per credential category
- Full audit logging of every access event

---

## Access Control

The system applies privilege filtering based on the requesting persona:

| Role | Permissions |
|------|-------------|
| Admin | Full access — all agents, all operations |
| HR / Senior Developer | DB read access, Git operations, knowledge base, credentials |
| Junior / Intern | Knowledge base only, limited Git (branch creation, PR view) |

Role is determined by the Mattermost user group at request time.

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Workflow Orchestration | n8n (self-hosted) |
| LLM / Intent Routing | Google Gemini |
| Vector Store (RAG) | Pinecone |
| Chat Interface | Mattermost |
| Git Operations | GitHub API |
| CI/CD Trigger | Jenkins API |
| Infrastructure | Ubuntu, Docker, Nginx |

---

## AI Components

- **Intent Classification** — Gemini routes each message to the correct agent using structured system prompts and few-shot examples
- **Output Formatting** — structured prompts enforce consistent, parseable responses (tables, lists, JSON)
- **RAG Retrieval** — Pinecone vector store queried for company-specific context before responding
- **Tool/Function Calling** — agents autonomously invoke APIs as tools based on LLM reasoning

---

## Security Considerations

- All credentials stored in n8n credential vault — never in workflow nodes
- Password vault uses hashing + reversible encryption — plaintext never at rest
- RBAC enforced at message routing layer — not just UI level
- Every credential access logged with timestamp, user, and action
- Sensitive operations require confirmation before execution

---

## Results

- Reduced repetitive manual developer operations across internal workflows
- Centralized Git, DB, DevOps, and knowledge operations into a single interface
- Eliminated context switching between GitHub, terminal, and documentation
- Role-based system prevented unauthorized access to sensitive infrastructure


<!-- ## Demo -->

<!-- Add Mattermost screenshot here -->
<!-- Add workflow diagram screenshot here -->
<!-- Add demo video link here -->

---

## How to Import

1. Import `workflow.json` into your n8n instance
2. Set up the following credentials in n8n credential vault
3. Configure Mattermost webhook
4. Embed your internal documents into Pinecone
5. Activate workflow

## Environment Variables

| Variable | Description |
|----------|-------------|
| `GEMINI_API_KEY` | Google Gemini API key |
| `PINECONE_API_KEY` | Pinecone vector database key |
| `PINECONE_INDEX` | Name of your Pinecone index |
| `MATTERMOST_WEBHOOK_URL` | Mattermost incoming webhook |
| `MATTERMOST_BOT_TOKEN` | Mattermost bot token |
| `GITHUB_TOKEN` | GitHub personal access token |
| `JENKINS_URL` | Jenkins server URL |
| `JENKINS_TOKEN` | Jenkins API token |
| `DB_HOST` | Database host |
| `DB_USER` | Database user |
| `DB_PASSWORD` | Database password |

---

## Future Improvements

- Add Slack support alongside Mattermost
- Expand DBOps to support PostgreSQL and MongoDB
- Add natural language query explanation before execution
- Implement approval workflow for destructive operations (DROP, DELETE)

---

> **Note:** Source code and workflow JSON contain internal credentials and company-specific configurations. Core workflow logic is documented here. Available for live walkthrough during interview process.
