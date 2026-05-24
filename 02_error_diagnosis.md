# Prompt: Error Diagnosis
**Use when:** You have a test failure, TypeScript error, or runtime crash and need the root cause — not just a fix.

---

## Template

```
I have [N] errors from running [command].

Here is the full output:
[paste complete error log — never summarize it, paste the raw output]

Here are the relevant files:
[paste every file mentioned in the error — not just the line that errored]

Do the following:
1. Group the errors by ROOT CAUSE, not by file
   (10 errors often have 1-2 root causes — identify those first)
2. For each root cause, explain WHY it happened in plain English
3. Give the fix in order — fix root causes first, symptoms will resolve automatically
4. If a fix to one root cause will resolve multiple errors, say so explicitly
5. Do not change any logic that isn't related to the error
6. After your fixes, tell me what command to run to verify all errors are resolved
```

---

## Worked example from this project

> 18 TypeScript errors across 13 files
> Root cause analysis found only 4 causes:
> - COLORS export renamed (7 errors)
> - @expo/vector-icons types missing (6 errors)
> - state.auth.user didn't exist (1 error)
> - 3 logic bugs in existing screens (4 errors)

---

## Key rules to always include
- "Group by root cause, not by file" — prevents fixing symptoms instead of causes
- "Paste every file mentioned" — Claude cannot diagnose with only the error line
- "Do not change logic unrelated to the error" — prevents collateral breakage

---

## Variant: Runtime bug (app behaves wrong, no error log)

```
My app is doing [X] but should do [Y].

There is no error in the console. The bug is behavioral.

Here are the files involved:
[paste all files in the data/navigation flow]

Trace the exact flow from [user action] to [expected outcome] and identify
where the flow breaks. Check these specific things:
- Redux state: what gets dispatched and what the reducer does with it
- Navigation: what condition controls which screen is shown
- API response: what field name the backend returns vs what the frontend reads

Do not suggest adding console.log — identify the bug from the code directly.
```

> Used when: login succeeded but stack never switched. Root cause: setToken reducer
> set state.token but never set state.isAuthenticated = true.
