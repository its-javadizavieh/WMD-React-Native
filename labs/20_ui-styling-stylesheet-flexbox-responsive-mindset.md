# Lab 20 – UI styling: StyleSheet, flexbox e responsive

## Obiettivo

- Layout responsive con `useWindowDimensions`.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Layout responsive con `useWindowDimensions`. Flexbox: colonna su mobile, riga su tablet.

> **Perché questo lab:** esercitare i pattern della lezione 20 in una mini-app concreta.

## Cosa imparerai

1. Come usare `useWindowDimensions` per rilevare la larghezza.
2. Come cambiare layout con un breakpoint (`width >= 600`).
3. Come usare `flexDirection: "row"` vs `"column"`.
4. Come definire spacing tokens per coerenza.

## Passi

1. **Avvia progetto** — verifica che l'app parta.
2. **Breakpoint** — `const isWide = width >= 600` tramite `useWindowDimensions()`.
3. **Layout condizionale** — `flexDirection: isWide ? "row" : "column"`.
4. **Spacing tokens** — `const SPACING = { sm: 4, md: 8, lg: 16 }` usati negli stili.
5. **Due card** — Mostrate in colonna su mobile, in riga su tablet.
6. **Edge case** — Testo lungo che wrappa correttamente.

## Screenshot attesi

**Layout mobile**

![Lab 20 - Layout mobile](imgs/lab_20_mobile.png)

**Layout tablet**

![Lab 20 - Layout tablet](imgs/lab_20_tablet.png)


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

- useWindowDimensions react native
flexbox responsive react native
stylesheet flexbox column row
