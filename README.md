# Real-Time Organ Donation Match & Allocation (Rule-Based)

Hackathon-ready reference implementation of a **real-time, event-driven, rule-based** organ allocation system.

## What this includes

- **Donor entry system** (real-time donor ingestion)
- **Recipient waiting list** (urgency + waiting time)
- **Strict rule-based matching** (organ type + blood group compatibility; no ML)
- **Priority-based allocation**:
  - Higher urgency wins
  - Tie-breaker: longer waiting time wins
  - Deterministic selection
- **Atomic allocation** (no duplicate assignments; consistent)
- **Real-time notifications** (WebSocket events)
- **Live dashboard** (HTML page with live updates)

## Quick start (Windows / PowerShell)

```powershell
cd "d:\Downloads\New folder"
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Open:
- Dashboard: `http://127.0.0.1:8000/`
- API docs (Swagger): `http://127.0.0.1:8000/docs`

## Core rule summary

- **Organ must match exactly** (e.g. kidney donor → kidney recipient)
- **Blood compatibility** uses standard ABO RBC transfusion compatibility:
  - O → O, A, B, AB
  - A → A, AB
  - B → B, AB
  - AB → AB

## Useful flows

1) Create recipients (waiting list)
2) Post a donor (triggers allocation attempt)
3) Watch real-time events on the dashboard (allocation + notifications)

## Notes / constraints

- This version uses an **in-memory store** for speed and simplicity (perfect for a 3-hour hackathon demo).
- Deterministic ordering ensures fairness and reproducibility.
- You can swap the store for a real database later without changing the rules engine.

