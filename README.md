# My Claude Prompt Library
Extracted from: MindCare Mental Health App project
Use these as starting templates — fill in the brackets, paste your files, send.

---

## The one rule that makes all of these work

**Paste first, ask second.**
Every prompt below has a `[paste your file]` placeholder.
Fill it in BEFORE sending. Never describe a file in words when you can paste it.
This single habit will halve the time it takes to get a useful answer.

---

## Prompt index

| # | File | Use when |
|---|---|---|
| 01 | `01_phase_breakdown.md` | Planning a new feature or milestone |
| 02 | `02_error_diagnosis.md` | Test failures, TypeScript errors, runtime bugs |
| 03 | `03_visual_rebuild.md` | Redesigning a screen without breaking its logic |
| 04 | `04_test_generation.md` | Writing pytest or Jest tests for completed features |
| 05 | `05_walkthrough_analysis.md` | Analyzing a progress doc to find what to do next |
| 06 | `06_backend_endpoint.md` | Adding or modifying a FastAPI endpoint |
| 07 | `07_qa_checklist.md` | Verifying a completed feature actually works |
| 08 | `08_design_system.md` | Setting up theme/colour tokens for a new UI |

---

## Session starter — paste this at the start of every new conversation

```
## Project context
App: [name and purpose in one sentence]
Stack: [Frontend stack] + [Backend stack]
Last completed: [feature or phase name]
Current task: [what you're about to build]
Known issues: [anything broken or deferred — "none" if clean]

## Key constraints
- [e.g. Expo SDK 55 — use npx expo install, not npm install]
- [e.g. pytest-asyncio strict mode — use @pytest_asyncio.fixture]
- [e.g. TypeScript strict mode — check with ./node_modules/.bin/tsc --noEmit]
- [e.g. Windows + Android emulator — always use npx expo start --tunnel]

## Files relevant to today's task
[paste 1-3 files that are most relevant to what you're doing]
```

---

## Workflow that worked in the MindCare project

```
1. Paste walkthrough → get phase plan (prompt 05 + 01)
2. Confirm plan → get phase prompts one at a time
3. Run each prompt → paste output into project
4. Run: ./node_modules/.bin/tsc --noEmit after EVERY phase
5. Paste errors → diagnose (prompt 02)
6. When phase is done → run QA checklist (prompt 07)
7. Paste checklist results with [!] items back to Claude
8. Fix failures → re-run failed checks only
9. Move to next phase
```

---

## Red flags — when to stop and replan

If any of these happen, don't push forward. Paste the situation and ask for a replan:

- TypeScript errors are increasing after fixes (root cause not found)
- A fix in one file breaks two other files (wrong abstraction)
- You've been on the same error for 3+ iterations (missing context — paste more files)
- A phase is taking 3x longer than estimated (scope was underestimated)
- You realize a later phase depends on something the current phase didn't build (dependency gap)

---

## Commands to always have ready

```bash
# TypeScript check (run after every phase)
./node_modules/.bin/tsc --noEmit

# Start dev server (Windows + Android emulator)
npx expo start --tunnel

# Run all backend tests
python -m pytest tests/ -v

# Run specific test file
python -m pytest tests/test_phase2.py -v

# Start database
docker-compose up -d

# Install RN package correctly (never npm install)
npx expo install [package-name]
```
