# Voyadecir Meta Repository

This repository is the **orchestration layer** for Voyadecir.

It exists to coordinate multiple independent repositories via **git submodules**.
It does NOT contain application logic.

---

## Repository Structure (Authoritative)

This repo contains the following submodules:

- `voyadecir-site`  
  Static HTML/CSS/JS frontend hosted on Render.

- `ai-translator`  
  FastAPI backend (Dockerized) handling translation, OCR orchestration,
  document parsing, and explanations.

- `azure-funcs-voyadecir`  
  Azure Functions for OCR routing and Azure Document Intelligence integration.

Each submodule is a **fully independent repository** with its own:
- history
- CI/CD
- deployment pipeline

---

## Non-Negotiable Rules

- **Do NOT move code between repositories**
- **Do NOT merge repositories**
- **Do NOT duplicate logic across repos**
- **Do NOT refactor architecture unless explicitly instructed**

The architecture is intentionally split and is considered **stable**.

---

## How Work Is Done

- All feature and bug work happens **inside the appropriate submodule**
- Pull requests are opened **in the submodule repository**
- This meta repo is updated only to bump submodule commit references

Think of this repo as a **playlist**, not the songs.

---

## Authoritative Documentation

The following files define system behavior and constraints:

- `AGENTS.md` — AI / agent rules and scope
- `TASKS.md` — Priority order and allowed work
- `OCR_DEBUG.md` — OCR behavior, retries, and fallback rules

If any document contradicts these, **these win**.

---

## Goal

Ship a reliable, bilingual Bills & Mail Helper and reach **$6k/month MRR**
by prioritizing:
- OCR reliability
- clarity
- monetization surfaces

This repo exists to prevent accidental complexity, not create it.
# voyadecir-meta
