# Lab 03 — Esercitazione — Environment setup hands-on: Expo workflow, CLI workflow, Android emulators, device testing

## Obiettivo

- Applicare i micro-argomenti della lezione 03 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Setup completo e verificabile: ogni studente deve riuscire ad avviare l’app e a fare debug di base su emulator o device. L’obiettivo è avere una checklist riusabile per tutto il corso.

## Step (numerati)

1. Verifica Node.js LTS e crea un progetto Expo.
2. Avvia l’app e documenta: come aprirla su emulator e come su device reale.
3. Esegui `npx expo start -c` e spiega quando serve.
4. Aggiungi un `console.log` in `useEffect` e verifica dove compare (terminal/device).
5. Se la rete dà problemi: prova `--tunnel` e annota pro/contro.
6. Consegna una checklist in fondo al file del lab (10 punti).

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

Nota Android (ADB):

- Se `adb devices` mostra `unauthorized`: sblocca il telefono, accetta il prompt di USB debugging, poi riprova.

Ordine di reset (prova in sequenza):

1) Reload dell’app
2) Restart Metro
3) `npx expo start -c`
4) Restart emulator/device

## Cleanup obbligatorio

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall’OS.
- Se hai usato storage locale: svuota i dati dell’app o rimuovi le chiavi salvate.

## Parole chiave Google (screenshot/guide)

- expo start --tunnel
- adb devices
- android studio avd manager
- expo go cannot connect to metro
