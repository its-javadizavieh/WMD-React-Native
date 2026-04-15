# Lab 17 – Gestione asincrona in mobile: loading / error states

## Obiettivo

- Simulazione success / failure con bottoni.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Simulazione success / failure con bottoni. Oggetto stato unico con campo `status`.

> **Perché questo lab:** esercitare i pattern della lezione 17 in una mini-app concreta.

## Cosa imparerai

1. Come usare un singolo oggetto stato `{ status, message }`.
2. Come simulare successo e fallimento con pulsanti.
3. Come usare `ActivityIndicator` per il loading.
4. Perché un oggetto stato unico evita stati incoerenti.

## Passi

1. **Avvia progetto** — verifica che l'app parta.
2. **Stato unico** — `const [state, setState] = React.useState({ status: "idle", message: "" })`.
3. **Funzione load(shouldFail)** — Imposta "loading", attende 800ms, poi success/error.
4. **UI condizionale** — `ActivityIndicator` per loading, messaggio per error/success.
5. **Due pulsanti** — "Retry (success)" e "Retry (fail)" per testare entrambi i flussi.

## Screenshot attesi

**Async workflow**

![Lab 17 - Async workflow](imgs/lab_17_main.png)


## Consegna minima

- App che parte su emulatore o device
- UI chiara e leggibile
- Un edge case gestito con un messaggio chiaro

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Cleanup completato

## Problemi comuni

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l'emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.
- Se l'app non si connette: controlla che PC e device siano sulla stessa rete (LAN).

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall'OS.
- Se hai usato storage locale: svuota i dati dell'app o rimuovi le chiavi salvate.

## Search terms

- react native loading state
activityindicator react native
