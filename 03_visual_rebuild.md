# Prompt: Visual Rebuild (Logic-Safe)
**Use when:** A screen works correctly but looks bad. You want to redesign it without risking the functionality.

---

## Template

```
Rebuild the visual layer of [FILE PATH].

Here is the current file: [paste it]

IMPORTANT — do NOT change any of the following:
- [list every piece of logic to preserve, e.g.:]
- API call to [endpoint]
- [State variable] and how it's updated
- Redux dispatch after [action]
- Navigation to [screen]
- [Function name] calls
- Error handling logic

Only replace:
- The JSX/render output
- StyleSheet definitions
- Any imports needed for new visual components

New visual design:
[describe the new design — or paste the design spec from a planning phase]

Colours come from: useTheme() hook — import from src/hooks/useTheme
All colours must use theme.XXX — no hardcoded hex values
Use StyleSheet with a makeStyles(theme: AppTheme) pattern:
  const makeStyles = (theme: AppTheme) => StyleSheet.create({ ... })
  Called inside the component: const styles = makeStyles(theme)

Export as default. Show the complete updated file.
```

---

## Worked examples from this project

**AssessmentScreen:** Kept all PHQ-9/GAD-7 logic, scoring, Redux dispatch.
Only replaced: flat buttons → card with tappable option rows, added progress bar, question fade animation.

**ResultsScreen:** Kept severity labels, crisis button logic, getCategoryMessage calls.
Only replaced: BarChart → animated SVG score rings, added severity chips, AI insight card.

**MoodScreen:** Kept POST /mood call, success/error states.
Only replaced: basic slider → large 72px live number, gradient track, contextual label.

---

## Why this prompt matters
Without "do NOT change X", Claude will often rewrite working logic while fixing the UI.
The explicit preservation list forces surgical changes only.
Always list every function call, API endpoint, and navigation action you depend on.

---

## Variant: Component-level visual upgrade

```
Update the visual styling of [COMPONENT NAME] only.
Here is the current component: [paste it]

Do not change the props interface — callers must not need to update.
Do not change any logic inside event handlers.
Only update: StyleSheet values, layout structure, animation (if adding).

New appearance: [describe]
Use theme from props: add theme: AppTheme to props if not already present.
```
