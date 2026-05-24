# Prompt: QA Checklist Generation
**Use when:** You've finished building a feature and need a structured way to verify it actually works before moving on.

---

## Template

```
Generate a manual QA checklist for [FEATURE NAME] in my [platform] app.

The checklist must cover:

1. NAVIGATION
   - Every screen transition in both directions (forward and back)
   - Cold start behavior (what appears first)
   - What happens after successful [action] (login/submit/etc)

2. VALIDATION  
   - Empty form submission (all errors appear simultaneously)
   - Each field with invalid data (correct error message appears)
   - Each field with valid data (error clears immediately on change)
   - Confirm no API calls fire when validation fails

3. API INTEGRATION
   - Happy path (correct data, correct server response)
   - Each error response the server can return (401, 400, 422, 500)
   - Network off scenario
   - Confirm no native Alert.alert popups — all errors inline

4. STATE MANAGEMENT
   - After [action], verify Redux state is correct
   - After app restart, verify persistent state reloads correctly

5. KEYBOARD AND LAYOUT
   - Tap first input — keyboard appears, content scrolls up
   - Tab through all inputs via return key
   - Last input return key triggers form submission
   - Layout correct on small screen (5-inch) and large screen (6.5-inch)

Format as GitHub-flavored markdown with [ ] checkboxes.
Group by section. Each item should be a single testable action with
a clear expected result — not vague ("looks correct").

Environment note at top:
> npx expo start --tunnel · Docker backend running · Android emulator
```

---

## Worked example from this project

Auth flow checklist covered 6 sections, 42 checks.
Key catches it found:
- Back button on Login didn't work (back button on Register did — narrowed to LoginScreen specifically)
- Successful login didn't switch stacks (pointed to Redux isAuthenticated issue)
- Offline error showed as Alert instead of inline card

---

## How to use the checklist output

Mark results with:
- `[x]` = passed
- `[!]` = failed — paste back to Claude with what you observed
- `[-]` = skipped (explain why)

When you paste failed items back:
```
These checks failed:
[!] Back button on Login returns to WelcomeScreen
[!] Successful login: main app stack appears

What I observed:
- Back button: nothing happens when tapped
- Login: API returns 200, console shows token, but screen stays on Login
```
> This format gives Claude everything needed to diagnose without asking follow-up questions.
