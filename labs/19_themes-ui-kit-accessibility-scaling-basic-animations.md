# Lab 19 - Temi, accessibilità e feedback pressione (Italian Meals App)

## Obiettivo

- Tema **light / dark** con design tokens e `ThemeContext`.
- `createSharedStyles(theme)` per colori adattivi (testo leggibile in entrambi i temi).
- Accessibilità su card e pulsanti; feedback `Pressable` su pressione.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale
- **Lab 18 completato** (StyleSheet condiviso)

## Scenario

Continua la **Italian Meals App**. In **Impostazioni** l'utente attiva il tema scuro con uno `Switch`; tutta l'app (lista, dettaglio, preferiti) deve restare leggibile. Su ogni `MealCard` aggiungi `accessibilityLabel` e feedback visivo al tocco.

> **Perché questo lab:** checkpoint progetto finale - almeno 2 accorgimenti accessibilità visibili + tema opzionale in Impostazioni.

## Cosa imparerai

1. Come definire `lightTheme` / `darkTheme` in `theme/colors.ts`.
2. Come creare `ThemeContext` con `toggleTheme` e persistenza opzionale (`app:v1:theme`).
3. Come usare `accessibilityRole="button"` e `accessibilityLabel` su `MealCard`.
4. Come dare feedback con `pressed && styles.pressedFeedback` su `Pressable`.
5. Come usare `maxFontSizeMultiplier` su titoli lunghi.

## Passi

1. **theme/colors.ts** - `AppTheme` con `colors.text`, `background`, `border`, `primary`, ecc.
2. **context/ThemeContext.tsx** - `theme`, `toggleTheme`; carica/salva modo con `services/storage.ts` (`THEME_KEY = "app:v1:theme"`).
3. **createSharedStyles(theme)** - aggiorna tutti i colori da `theme.colors`, non valori hardcoded.
4. **SettingsScreen** - `Switch` «Tema scuro» + conteggio preferiti + logout.
5. **MealCard** - `accessibilityRole="button"`, `accessibilityLabel={\`Apri ${meal.strMeal}\`}`, opacity su pressed.
6. **FavoriteButton** - stesso pattern accessibile; icona ♡/♥ con contrasto adeguato.
7. **Edge case** - Aumenta font size nelle impostazioni Android → verifica che titoli non escano dal layout (`maxFontSizeMultiplier={1.4}`).

## Screenshot attesi

**Tema chiaro - lista piatti leggibile**

![Lab 19 - Tema light](../labs/imgs/lab_19_theme_light.png)

**Tema scuro - testo e card visibili**

![Lab 19 - Tema dark](../labs/imgs/lab_19_theme_dark.png)

## Consegna minima

- Toggle tema in Impostazioni con UI coerente
- Almeno 2 accorgimenti a11y (es. `accessibilityLabel` su card + `accessibilityRole="header"` su titolo)
- Feedback pressione su `MealCard` / pulsanti
- Nessun testo bianco su sfondo bianco (o invisibile in dark mode)

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] `ThemeContext` + `useTheme()` nelle screen
- [ ] `createSharedStyles(theme)` usato ovunque
- [ ] Edge case font size grande
- [ ] Screenshot in Google Doc (riga **Lab 19**)

## Problemi comuni

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se testo invisibile in dark mode: usa `theme.colors.text`, non `#000` fisso.
- Se il tema non persiste: verifica `saveThemeMode` in `ThemeContext` al toggle.

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.

## Search terms

- react native dark theme context
- accessibilityLabel flatlist
- maxFontSizeMultiplier react native
- pressable pressed opacity
