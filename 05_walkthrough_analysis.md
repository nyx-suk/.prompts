# Prompt: Walkthrough Analysis + Next Steps
**Use when:** You have a commit walkthrough, implementation summary, or progress doc and need to know what to do next.

---

## Template

```
Here is a walkthrough of the current project state:

[paste walkthrough document in full]

Analyze this and tell me:

1. WHAT IS ACTUALLY BUILT vs WHAT IS CLAIMED
   - List features the walkthrough says are complete
   - Flag any claims that don't match what was likely implemented
     (e.g. "HIPAA compliant" but no encryption mentioned)
   - Flag any gaps between the stated goals and the completed work

2. WHAT IS BROKEN OR RISKY RIGHT NOW
   - Deprecated code that will break in future versions
   - Security issues
   - Missing error handling
   - Anything that would fail in a live demo

3. WHAT IS THE LOGICAL NEXT STEP
   - Order by: blockers first, then core features, then polish
   - Consider dependencies (what breaks if we skip something)

4. WHAT IS OUT OF SCOPE FOR MVP
   - Features mentioned but not needed for a working demo
   - Things to defer to "future work"

After your analysis, give me a prioritized phase plan.
Do not write any code yet.
```

---

## Worked example from this project

> Pasted walkthrough of Commit 3 (PHQ-9/GAD-7 integration)
> Analysis caught:
> - `@app.on_event("startup")` deprecation warning
> - `progress` table existed but unused (repurposed for mood tracking)
> - Frontend components not yet tested against live backend
> - BERT integration claimed but not yet built

---

## Variant: Review an implementation plan someone else wrote

```
Here is an implementation plan: [paste it]

Critique it from the perspective of a senior engineer.
Identify:
1. What it gets right
2. Critical gaps (things it doesn't cover that will cause problems)
3. Wrong assumptions (things it assumes exist that may not)
4. Missing dependencies (things that need to be built first)
5. Scope creep (things that sound important but aren't needed for MVP)

Then rewrite the plan with these gaps filled.
Keep the same goal but make it production-realistic.
```

> Used when: Original Welcome screen plan only covered 1 of 3 auth screens,
> had no Redux integration, no form validation, and ignored Expo SDK constraints.
> Rewrite expanded to 8 phases covering all auth screens + shared infrastructure.
