# OCR_DEBUG.md — Authoritative OCR Behavior

This file overrides **all other OCR assumptions**.

Primary OCR: **Azure Document Intelligence Read (prebuilt-read)**  
Fallback OCR: **Tesseract (last resort only)**

---

## Required Behavior (Non-Negotiable)

Every OCR request MUST return structured metadata:

- engine_used: azure_primary | fallback
- confidence: 0–1
- stages:
  - upload_parse
  - pdf_to_image
  - preprocess
  - azure_call
  - fallback_call
  - extraction
- user_facing_error (EN/ES if failure)

Generic “server error” responses are forbidden.

---

## Retry Rules

- Azure OCR analyze: 2–3 retries
- Exponential backoff
- Hard timeout safety

---

## Fallback Rules

Fallback ONLY when:
- Azure errors or times out
- confidence < OCR_CONFIDENCE_THRESHOLD (default 0.75)

Never fallback “just in case”.

---

## Preprocessing Rules

### PDFs
- Convert to images at 300 DPI via poppler

### Phone Photos
- grayscale
- deskew
- adaptive threshold
- denoise
- mild sharpen

---

## Quality Warnings

If confidence is low:
- Return warning
- Suggest retake tips
- Always bilingual (EN/ES)

---

## Environment Variables

Required:
- AZURE_DI_ENDPOINT
- AZURE_DI_API_KEY
- AZURE_DI_API_VERSION
- AZURE_DI_MODEL=prebuilt-read

Optional:
- OCR_CONFIDENCE_THRESHOLD=0.75
- DEBUG_OCR=false

---

## Acceptance Criteria

- ≥90% word recall on clean PDFs
- ≥75% usable extraction on phone photos
- stage errors visible on any failure
- fallback triggers only per rules above

