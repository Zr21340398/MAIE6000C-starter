# Week 3 Submission — Individual Readiness Lab

## Student information

- Name: <ZHOU RAN>
- Student ID: <21340398>
- Repository: https://github.com/Zr21340398/MAIE6000C-starter
- Checkpoint tag: `w03-readiness`
- Commit SHA: 

## 1. What I changed

I updated the `CaseCreate` schema to strip leading and trailing whitespace
before validating minimum field lengths.

Previously, whitespace-only values could pass validation and then be stored as
empty strings. The API now rejects these requests with HTTP 422.

I also added an integration regression test for this behaviour.

## 2. Files touched

- `services/common/schemas.py`
- `tests/integration/test_api_case_flow.py`
- `submissions/week03/README.md`

## 3. How I verified it

- Before the change, a whitespace-only POST request returned HTTP 201 and
  created a case with empty title and description.
- After the change, the same request returned HTTP 422.
- `pytest -q tests/integration/test_api_case_flow.py::test_create_case_rejects_whitespace_only_input`
  - Result: `1 passed`
- `pytest -q tests/unit tests/integration`
  - Result: `5 passed`
- `ruff check services tests`
  - Result: `All checks passed!`

## 4. Known limitations or notes

This change only affects case creation input validation. It does not modify the
database schema, worker, or rule-based triage service.

## 5. AI Use Statement

OpenAI Codex was used to analyse the assignment requirements, suggest a bounded validation change, and plan the verification workflow. 