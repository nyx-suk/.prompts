# Prompt: Backend Endpoint Creation (FastAPI)
**Use when:** You need to add a new API endpoint to an existing FastAPI backend.

---

## Template

```
Add a new endpoint to my FastAPI backend.

Here is my current backend/main.py: [paste it]
Here is my current backend/models.py: [paste it]

Endpoint spec:
  Method + path: [e.g. POST /mood]
  Auth required: Yes — use the existing get_current_user dependency
  Request body (Pydantic schema): 
    [field: type, constraints]
  Response (Pydantic schema):
    [field: type]
  Logic:
    1. [step by step what it does]
    2. [validation rules]
    3. [what it reads/writes to DB]
  Error cases:
    [status code]: [when this happens]

Database:
  Table: [existing or new]
  If new column needed: add to models.py and note that 
    docker-compose down && docker-compose up -d is required to apply

Rules:
- Use the existing SessionLocal and get_db dependency for DB sessions
- Use the existing get_current_user dependency for auth
- Follow the existing code style (check how other endpoints are written)
- Add the Pydantic schemas near the top of main.py with existing schemas
- Do not change any existing endpoints
- Show only the new endpoint code and new schemas — not the entire file
  unless the change is to models.py (show that in full)
```

---

## Worked examples from this project

**POST /mood:** Validated mood_score 1-10, saved to Progress table with user_id.
**GET /mood/history?days=30:** Filtered by date range, ordered descending, returned list.
**GET /assessments/history?days=30:** Ordered ascending (for charting left-to-right).
**POST /ml/classify:** Async httpx call to HuggingFace, 10s timeout, graceful 503 on failure.
**GET /health:** Simple health check returning status + timestamp.

---

## Variant: Modify an existing endpoint

```
Modify the existing [METHOD] [PATH] endpoint in backend/main.py.

Here is the current endpoint: [paste just that function]

Change:
- [specific change 1]
- [specific change 2]

Do NOT change:
- [what must stay the same]

The change must be backwards compatible — any existing frontend
calls to this endpoint must still work without changes.

Show only the updated endpoint function.
```

---

## Database migration note (always include this)

```
If this change requires a new table or new column:
1. Show the updated models.py
2. Include this note at the top:
   "Run: docker-compose down -v && docker-compose up -d to apply schema changes locally.
    On Render: the DB migration will apply automatically on next deploy."
3. Note any data that will be lost (down -v wipes volume)
```
