# Soluzioni dei Lab

Questa cartella contiene la **soluzione di riferimento** per ogni lezione del corso React Native.

## Come usare queste soluzioni

1. **Prima prova da solo** — completa il lab seguendo le istruzioni nella cartella `labs/`.
2. **Confronta il tuo codice** — apri la soluzione corrispondente e confronta approccio, struttura e stile.
3. **Copia nel progetto** — ogni soluzione è un file `App.tsx` completo e funzionante. Puoi copiarlo direttamente nel tuo progetto Expo per testarlo.

> **Attenzione:** copiare le soluzioni senza capirle non ti aiuterà all'esame. Usa le soluzioni per imparare, non per saltare il lavoro.

## Struttura di ogni soluzione

Ogni file `.md` contiene:

- **Cosa mostra la soluzione** — breve descrizione di cosa fa il codice.
- **Codice** — il codice `App.tsx` completo (e file aggiuntivi dove necessario).

## Pattern comuni nelle soluzioni

- **`SafeAreaProvider` + `SafeAreaView`** — da `react-native-safe-area-context`, evita che il contenuto finisca sotto la status bar.
- **`Pressable` con stili visibili** — bordi, bordi arrotondati e sfondo grigio per rendere i pulsanti riconoscibili.
- **Nessun `interface`** — i tipi delle props si scrivono inline: `{ name }: { name: string }`.
- **Un solo file** — la maggior parte dei lab usa un singolo `App.tsx` per semplicità.

## Indice

| Lab | Argomento |
|-----|-----------|
| [01](01_solution-introduction-rn-vs-react-js-pros-cons-architecture-overview-setup-overview-expo-cli-emulators.md) | Introduzione a React Native, setup Expo |
| [02](02_solution-bridge-architecture-and-native-rendering-concepts-limitations.md) | Bridge, re-render, FlatList |
| [03](03_solution-environment-setup-hands-on-expo-workflow-cli-workflow-android-emulators-device-testing.md) | Ambiente di sviluppo, emulatori |
| [04](04_solution-mobile-problem-solving-and-app-oriented-design.md) | Problem solving mobile, design |
| [05](05_solution-modular-architecture-in-react-native-modules-components-screens.md) | Architettura modulare, screen e componenti |
| [06](06_solution-core-vs-third-party-libraries-dependencies-and-versioning.md) | Librerie core vs terze parti |
| [07](07_solution-react-native-base-components-part-1.md) | Componenti base (parte 1) |
| [08](08_solution-props-events-binding-base-components-part-2.md) | Props, eventi, binding (parte 2) |
| [09](09_solution-state-with-usestate-controlled-components-intro.md) | State con useState |
| [10](10_solution-useeffect-async-side-effects-and-cleanup.md) | useEffect, side effects, cleanup |
| [11](11_solution-forms-in-mobile-controlled-forms-and-patterns.md) | Form controllati |
| [12](12_solution-midterm-exam-guided-review-covers-lessons-01-11.md) | Revisione guidata (midterm) |
| [13](13_solution-react-navigation-setup-and-core-concepts.md) | React Navigation setup |
| [14](14_solution-route-params-and-dynamic-navigation.md) | Route params, navigazione dinamica |
| [15](15_solution-advanced-navigation-and-deep-linking.md) | Navigazione avanzata, deep linking |
| [16](16_solution-rest-calls-with-fetch-axios-async-handling.md) | REST con fetch/axios |
| [17](17_solution-asynchronous-workflows-in-mobile-loading-error-states.md) | Workflow asincroni, loading/error |
| [18](18_solution-local-persistence-with-asyncstorage.md) | Persistenza locale, AsyncStorage |
| [19](19_solution-global-state-context-redux-zustand-tradeoffs-and-patterns.md) | Stato globale, Context/Zustand |
| [20](20_solution-ui-styling-stylesheet-flexbox-responsive-mindset.md) | Styling, StyleSheet, Flexbox |
| [21](21_solution-themes-ui-kit-accessibility-scaling-basic-animations.md) | Temi, UI kit, accessibilità, animazioni |
| [22](22_solution-native-features-camera-location-sensors-permissions-and-security.md) | Feature native, permessi, sicurezza |
| [23](23_solution-notifications-background-tasks-final-exam-individual-mini-project-evaluation.md) | Notifiche, background tasks, progetto finale |