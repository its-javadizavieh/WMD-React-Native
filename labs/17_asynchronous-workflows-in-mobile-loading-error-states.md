# Lab 17 — Esercitazione — Asynchronous workflows in mobile (loading/error states)

## Obiettivo

- Applicare i micro-argomenti della lezione 17 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Prendi una schermata asincrona (es. una fetch da Lesson 16 o una qualsiasi operazione async) e rendila *prevedibile* tramite una gestione stati chiara.

## Step (numerati)

1. Avvia l’app e scegli una schermata con async (fetch o altra operazione).
2. Definisci uno stato unico per la UI (es. `loading/error/empty/success`).
3. Implementa una funzione `load()` che:

- imposta `loading`
- gestisce `success`
- gestisce `empty` (se applicabile)
- gestisce `error` con messaggio

1. Aggiungi un pulsante Retry che richiama `load()`.
2. Edge case obbligatorio: evita update di stato quando la schermata non è più montata (niente warning/bug da “stale update”).
3. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- App eseguibile su emulatore o device
- Stati async espliciti (loading/error/empty/success)
- Retry funzionante
- Edge case dimostrabile: niente update “stale” dopo navigazione/unmount

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
