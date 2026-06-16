# Lab 15 - REST calls e workflow asincroni con stati UI

## Obiettivo

- Carica dati da REST API con `fetch` e mostra in `FlatList`.
- Un solo oggetto stato con `status` (loading / error / success).
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h 30m

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Carica dati da JSONPlaceholder, incapsula fetch in `services/`, modella la UI con un singolo oggetto stato e pulsante Retry.

> **Perché questo lab:** esercitare i pattern della lezione 15 in una mini-app concreta.

## Cosa imparerai

1. Come usare `fetch` con controllo `res.ok`.
2. Come gestire errori HTTP (non trattarli come successo).
3. Come usare un singolo oggetto stato `{ status, items, message }`.
4. Come mostrare `ActivityIndicator`, errore con Retry e lista con `FlatList`.

## Passi

1. **Avvia progetto** - verifica che l'app parta.
2. **services/posts.ts** - `loadPosts()` con `fetch` da `jsonplaceholder.typicode.com/posts?_limit=5` e controllo `res.ok`.
3. **Stato unico** - `const [state, setState] = React.useState({ status: "idle", items: [], message: "" })`.
4. **load()** - Imposta `loading`, poi `success` o `error` con messaggio.
5. **UI condizionale** - `ActivityIndicator` per loading, messaggio + Retry per error, `FlatList` per success.
6. **Edge case** - Simula errore (URL sbagliata) e mostra Retry funzionante.

## Screenshot attesi

**Posts caricati - dati da REST API con fetch**

![Lab 15 - Posts caricati](imgs/lab_15_main.png)

**Stato errore - errore HTTP con pulsante Retry**

![Lab 15 - Stato errore](imgs/lab_15_error.png)

**Workflow asincrono - stati loading / success / error**

![Lab 15 - Workflow asincrono](imgs/lab_15_workflow.png)

## Consegna minima

- App che parte su emulatore o device
- UI chiara con un solo stato attivo alla volta
- Retry funzionante dopo errore HTTP

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Fetch con controllo `res.ok`
- [ ] Stati loading / error / success espliciti
- [ ] Edge case gestito con messaggio chiaro
- [ ] Cleanup completato

## Problemi comuni

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l'emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.
- Se l'app non si connette: controlla che PC e device siano sulla stessa rete (LAN).

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.

## Search terms

- fetch api react native
- jsonplaceholder posts
- react native loading state
- activityindicator react native
