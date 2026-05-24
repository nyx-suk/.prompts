# Prompt: Test Generation
**Use when:** You need pytest (backend) or Jest (frontend) tests for completed features.

---

## Backend: pytest + httpx Template

```
Write a pytest test file at tests/[test_file_name].py for my FastAPI backend.

Environment:
- pytest-asyncio in STRICT mode (pytest 9)
- Use @pytest_asyncio.fixture for ALL async fixtures (not @pytest.fixture)
- Use @pytest.mark.asyncio on all async test functions
- HTTP client: httpx.AsyncClient with base_url="http://localhost:8000"
- Database: PostgreSQL via psycopg2 for direct cleanup queries

Here are the endpoints to test:
[list each endpoint with method, path, auth requirement, expected behavior]

Here is the relevant backend code:
[paste main.py sections for each endpoint]

Write tests for:
[list each test case — be specific about inputs and expected outputs]

Fixture requirements:
1. auth_token fixture (module scope):
   - POST /auth/register with TEST_EMAIL and TEST_PASSWORD
   - Returns the token string
   - Mark with @pytest_asyncio.fixture(scope="module")

2. cleanup fixture (autouse=True, module scope):
   - Runs BEFORE tests: delete test user if exists (idempotent)
   - yield
   - Runs AFTER tests: delete all records created during tests
   - Uses psycopg2 direct connection with:
     host=localhost, dbname=[db], user=[user], password=[pass], port=5432
   - try/finally to ensure cleanup always runs

3. For any fixture that depends on auth_token:
   - Must also be @pytest_asyncio.fixture
   - In STRICT mode, async fixtures cannot depend on sync fixtures

Verify all edge cases:
- Happy path (valid data, assert 200 + response shape)
- Validation failures (invalid data, assert 4xx)  
- Auth failures (no token or invalid token, assert 401)
- Empty results (valid request but no data, assert 200 + empty list)
```

---

## Frontend: Jest + TypeScript Template

```
Write Jest tests at [file path] for [module name].

Here is the module: [paste scoring.ts / utility file]

This module has no side effects — pure functions only. No mocking needed.

Write tests using describe/it blocks:

describe('[function name]'):
  Test every boundary value:
  - Minimum valid input
  - Maximum valid input  
  - Each threshold where output changes
  - Edge cases (0, null-like values, maximum)

Rules:
- Use exact boundary values from the clinical/business spec
- Test name should state the input AND expected output:
  it('returns "Severe" for PHQ-9 score 20') not it('works for high scores')
- No beforeEach needed for pure functions
- Assert the exact return value, not just truthy/falsy

Show the complete test file.
```

---

## Worked examples from this project

**test_phase1.py:** Auth registration, login, questions (16 count, 9 depression + 7 anxiety), assessment submission.
**test_phase2.py:** Mood POST validation (0 and 11 both invalid), history filtering by days, assessment history ordering, ML classify response shape.
**scoring.test.ts:** All PHQ-9 boundary values (0,4,5,9,10,14,15,19,20,27), all GAD-7 boundaries, checkHighRisk two-trigger system.

---

## Critical rules for pytest-asyncio strict mode (from this project)

```
# ALWAYS use pytest_asyncio.fixture for async fixtures
import pytest_asyncio

@pytest_asyncio.fixture(scope="module")  # ← NOT @pytest.fixture
async def auth_token():
    ...

# ALWAYS mark async tests
@pytest.mark.asyncio
async def test_something(auth_token):
    ...

# Pre-clean before yield, post-clean after yield
@pytest_asyncio.fixture(autouse=True, scope="module")
async def cleanup():
    # delete test data that might exist from previous run
    yield
    # delete test data created during this run
```
