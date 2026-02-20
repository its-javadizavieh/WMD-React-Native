# Lab 14 — Esercitazione — Route params and dynamic navigation

## Obiettivo

- Applicare i micro-argomenti della lezione 14 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Partendo da un’app con navigazione (o creandola da zero), implementa un flusso **lista → dettaglio** dove la schermata di dettaglio dipende da un **route param** (tipicamente un `id`).

L’obiettivo è dimostrare che:

- navighi passando un param valido
- la schermata di dettaglio **valida** il param (input non affidabile)
- gestisci esplicitamente: param mancante/invalid e id non trovato

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
1. Crea (o riusa) uno stack con `Home` (lista) e `Details` (dettaglio).
1. In `Home`, naviga a `Details` passando il minimo indispensabile (es. `{ id }`).
1. In `Details`, leggi il param da `route.params` e validalo:

    - id mancante o tipo sbagliato → stato “Param non valido” + pulsante Back

1. Edge case obbligatorio: gestisci `id` valido ma non presente nella sorgente dati → stato “Not found” + Back.
1. Aggiungi un modo per riprodurre l’errore (es. bottone “vai a Details senza param”).
1. Se utile, organizza in moduli: `screens/`, `components/`, `services/`.
1. Esegui una demo rapida (30–60 secondi) e annota cosa hai imparato.
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
