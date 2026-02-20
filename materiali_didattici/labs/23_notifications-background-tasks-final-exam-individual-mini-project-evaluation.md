# Lab 23 — Esercitazione — Notifications + background tasks; final exam (individual mini-project) evaluation

## Obiettivo

- Applicare i micro-argomenti della lezione 23 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Implementa una feature minima di **notifiche locali** (Expo Notifications) con permission-first UX.

In più, prepara il progetto per la **valutazione finale** (mini-progetto individuale): deve essere riproducibile, demo-able e con cleanup chiaro.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
1. Installa Expo Notifications e riavvia Metro.
1. Crea una schermata con UI a stati espliciti (esempio):

    - `idle` (spiega cosa farà)
    - `requesting` (permission/check)
    - `denied` (fallback + spiegazione)
    - `scheduled` (conferma)
    - `error` (messaggio + retry)

1. Permission-first flow:

    - controlla permessi
    - richiedi solo quando serve
    - gestisci denial senza bloccare l’app

1. Programma una notifica locale (es. tra 3–10 secondi) e mostra feedback in UI.
1. Edge case obbligatorio: permesso negato (e, su Android, assicurati che il canale esista).
1. Background constraints (nota scritta, 3 righe): perché la delivery non è garantita e come lo comunichi in UX.
1. Checklist “valutazione finale” (verifica almeno questi punti):

    - `npm ci` / install pulita
    - `npx expo start -c` funziona
    - `git status` pulito (o modifiche spiegate)
    - demo 30–60 secondi con edge case

1. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- App eseguibile su emulatore o device
- UI chiara e leggibile
- Almeno un edge case gestito in modo esplicito

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
