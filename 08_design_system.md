# Prompt: Design System + Theme Setup
**Use when:** Starting UI work on a new project, or adding dark/light theme switching to an existing one.

---

## Template: Theme tokens file

```
Create src/theme/colors.ts for a React Native app (Expo SDK [version], strict TypeScript).

I need both a dark and light theme.

Create an AppTheme interface with these token categories:
- Backgrounds: background, surface, surfaceSecondary
- Brand: primary, primaryLight, primaryDark
- Text: textPrimary, textSecondary, textHint
- Borders: border, borderFocus
- Semantic: error, errorSurface, warning, warningSurface, success
- Navigation: tabBar, tabBarActive, tabBarInactive

Dark theme values: [paste your colour decisions]
Light theme values: [paste your colour decisions]

Rules:
- Use 'as const' on each theme object (literal types, not widened to string)
- Export type { AppTheme } for use in makeStyles functions
- Also export SPACING: { xs:4, sm:8, md:16, lg:24, xl:32, xxl:48 }
- Also export RADIUS: { input:10, button:28, card:16 }
- Named exports only, no default export
- No logic, no functions — pure data

The pattern screens will use:
  const makeStyles = (theme: AppTheme) => StyleSheet.create({ ... })
  // called inside component:
  const { theme } = useTheme()
  const styles = makeStyles(theme)
```

---

## Template: ThemeContext + Redux persistence

```
Create a theme switching system for React Native (Expo SDK [version], strict TypeScript).

Files to create:
1. src/context/ThemeContext.tsx — React context + ThemeProvider
2. src/hooks/useTheme.ts — convenience hook
3. src/store/settingsSlice.ts — Redux slice with themeMode + AsyncStorage persistence

ThemeProvider reads themeMode from Redux (state.settings.themeMode).
toggleTheme() dispatches to Redux, which persists to AsyncStorage.
On app start, loadThemeMode thunk reads AsyncStorage and sets Redux state.

All screens use: const { theme } = useTheme()
No screen ever imports DARK_THEME or LIGHT_THEME directly.
ThemeProvider wraps the app inside Redux Provider but outside NavigationContainer.

Show all three files.
```

---

## Worked example from this project

Dark theme (#0f1923 background) + light theme (#f0f7f6 background)
Toggle switch in SettingsScreen dispatches toggleTheme() → Redux → AsyncStorage
Persists across app restarts. Entire app re-renders when toggle fires.

---

## Colour palette that worked well for this project (mental health app)

```
Dark theme:
  background:      #0f1923   (dark navy — feels calm, premium)
  surface:         #162330   (elevated card)
  primary:         #00897b   (teal — clinical, trustworthy)
  primaryLight:    #4db6ac   (soft teal — accents)
  warning:         #ffb74d   (amber — moderate severity)
  error:           #ef5350   (red — severe/crisis)

Light theme:
  background:      #f0f7f6   (very light teal-white)
  surface:         #ffffff
  primary:         #00897b   (same — brand consistency)
  textPrimary:     #1a2e2b
```

---

## Styled component pattern for themed StyleSheets

```typescript
// Outside component — factory function
const makeStyles = (theme: AppTheme) => StyleSheet.create({
  container: {
    backgroundColor: theme.background,
    flex: 1,
  },
  card: {
    backgroundColor: theme.surface,
    borderRadius: RADIUS.card,
    borderWidth: 0.5,
    borderColor: theme.border,
    padding: SPACING.lg,
  },
})

// Inside component
export default function MyScreen() {
  const { theme } = useTheme()
  const styles = makeStyles(theme)   // recreated when theme changes
  return <View style={styles.container} />
}
```
