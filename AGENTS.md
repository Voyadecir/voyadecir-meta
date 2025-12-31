# AGENTS.md — Voyadecir AI & Agent Rules

This file defines **binding rules** for all AI assistance (Cursor, agents, tools).

These rules are not suggestions.

---

## Mission

Ship Voyadecir as a bilingual (EN/ES) **Translate + Bills & Mail Helper**.

Primary user: people receiving confusing or scary mail who need
**immediate understanding**, not just translation.

Revenue target: **$6k/month MRR ASAP** by shipping revenue surfaces first.

---

## Core Principles

1. **Reliability beats cleverness**
2. **Revenue surface before features**
3. **Minimalist UI, maximal clarity**
4. **Privacy-first by default**

---

## Architecture (Authoritative)

### Frontend
- Static HTML/CSS/JS
- Hosted on Render
- No secrets, no keys, no LLMs client-side
- EN/ES autodetect + manual toggle required

### Backend
- FastAPI on Render (Docker)
- Owns:
  - OCR orchestration
  - translation
  - explanations
  - agent logic

### Azure
- Azure Document Intelligence Read OCR = **primary**
- Azure OpenAI = **primary LLM**
- Azure Functions handle OCR routing

---

## Guardrails for AI / Agents

### Allowed Scope (RIGHT NOW)
- P0 tasks only (see TASKS.md)
- OCR stabilization
- retry, timeout, fallback hardening
- minimal UI polish strictly supporting P0

### Explicitly Not Allowed
- moving logic client-side
- introducing new architectures
- starting P1+ work
- adding heavy dependencies without instruction
- refactoring for “cleanliness” alone

---

## Style Rules

- Small, typed functions (Pydantic v2)
- Tenacity retries on all external calls
- Explicit errors, never silent failures
- EN/ES parity in user-facing messages

If unsure, **do less**.

