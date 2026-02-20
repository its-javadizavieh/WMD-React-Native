# Lab 16 — Esercitazione — REST calls with fetch / Axios; async handling

## Obiettivo

- Applicare i micro-argomenti della lezione 16 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Realizza una schermata che carica dati da una REST API e li mostra in UI.

Scegli UNA API tra queste (o equivalente):

- <https://jsonplaceholder.typicode.com/posts>
- <https://dummyjson.com/products>

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Crea un modulo `services/` con UNA funzione (es. `getPosts()` o `getProducts()`).
3. Implementa la chiamata con `fetch` (oppure Axios se preferisci):

- gestisci errori di rete
- gestisci HTTP non-2xx (non trattarli come successo)

1. Nella schermata, mostra stati espliciti:

- loading
- error (con pulsante Retry)
- empty (se lista vuota)
- success (lista)

1. Edge case obbligatorio: simula un errore (es. URL sbagliato) e mostra un messaggio chiaro.
2. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- App eseguibile su emulatore o device
- UI chiara e leggibile
- Almeno una schermata con dati REST + stati (loading/error/empty/success)
- Edge case dimostrabile (errore rete o HTTP non-2xx)

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Cleanup completato

## Troubleshooting rapido

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l’emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.
- Se l’app non si connette: controlla che PC e device siano sulla stessa rete (LAN).

## Cleanup obbligatorio

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall’OS.
- Se hai usato storage locale: svuota i dati dell’app o rimuovi le chiavi salvate.

## Parole chiave Google (screenshot/guide)

- expo start android emulator
- expo go cannot connect to metro
- react native metro bundler address already in use
- android emulator not starting virtualization
