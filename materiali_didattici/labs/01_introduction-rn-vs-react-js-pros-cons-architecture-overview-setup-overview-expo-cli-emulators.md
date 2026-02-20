# Lab 01 — Esercitazione — Introduction, RN vs React JS, pros/cons, architecture overview, setup overview (Expo/CLI/emulators)

## Obiettivo

- Applicare i micro-argomenti della lezione 01 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Crea la tua prima mini-app Expo e costruisci 1 schermata ‘About this app’ che spiega, con testo e layout, la differenza tra React Native e React JS.

## Step (numerati)

1. Crea un nuovo progetto Expo e avvialo (`npx expo start`).
2. Sostituisci il contenuto di `App` con una schermata che contiene: titolo, 2 paragrafi, 1 lista puntata.
3. Estrai un componente `Greeting` che riceve `name` via props e mostrane l’uso nella UI.
4. Aggiungi uno StyleSheet con: spacing coerente, testo grande per il titolo, centratura con flexbox.
5. Esegui la demo su device o emulatore e verifica Fast Refresh modificando una stringa.
6. Esegui cleanup obbligatorio e annota 3 problemi tipici di setup + soluzione.

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

Se la rete LAN è bloccata (VPN / Wi‑Fi isolato), prova:

- `npx expo start --tunnel`

## Cleanup obbligatorio

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall’OS.
- Se hai usato storage locale: svuota i dati dell’app o rimuovi le chiavi salvate.

## Parole chiave Google (screenshot/guide)

- npx create-expo-app
- expo start -c
- expo go cannot connect to metro
- android emulator not starting virtualization
