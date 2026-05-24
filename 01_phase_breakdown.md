# Prompt: Phase Breakdown
**Use when:** You have a feature or milestone to build and need it split into ordered, safe steps.

---

## Template

```
I am building [PROJECT NAME]. Here is my current state:

[paste walkthrough / summary of what's built]

I need to implement [FEATURE / MILESTONE].

Split this into phases with the following rules:
1. Each phase must have a single clear deliverable
2. List dependencies between phases (what must be done first)
3. Estimate time per phase
4. For each phase, list exactly which files are created (NEW) or changed (MOD)
5. Flag any phase that could break existing functionality
6. Include a verification step at the end of each phase so I know it's done correctly

My stack:
- Frontend: [your stack]
- Backend: [your stack]
- Key constraints: [e.g. Expo SDK 55, Windows, strict TypeScript]

Do not write any code yet. Just the plan.
After I confirm the plan, give me the prompts for each phase one at a time.
```

---

## Worked example from this project

> "Split this into phases and give prompts for each" (auth flow UI)
> Produced: 7 phases, 8 files, clear dependency order (tokens → components → screens → navigator)

---

## Key rules to always include
- "Do not write any code yet. Just the plan." — prevents Claude from jumping ahead
- "List dependencies between phases" — catches the #1 mistake: building screens before design tokens
- "Give me prompts one at a time" — prevents getting overwhelmed by 10 prompts at once
