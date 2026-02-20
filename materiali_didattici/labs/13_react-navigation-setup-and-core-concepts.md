# Lab 13 — Esercitazione — React Navigation: setup and core concepts

## Obiettivo

- Applicare i micro-argomenti della lezione 13 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Implementa una mini-app con **React Navigation** (stack) e **2 schermate**:

- `Home` (lista o contenuto semplice)
- `Details` (schermata di dettaglio)

La consegna è completata quando riesci a dimostrare il flusso **Home → Details → Back** in modo stabile.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Installa React Navigation (Expo workflow) e riavvia Metro.
3. Aggiungi `NavigationContainer` e uno stack navigator.
4. Crea `HomeScreen` e `DetailsScreen` e registrale nello stack.
5. Da Home, naviga a Details (es. al tap su un item) e aggiungi un pulsante Back.
6. Edge case obbligatorio: gestisci *uno* stato esplicito verificabile (es. lista vuota con messaggio dedicato).
7. Se utile, organizza in moduli: `screens/`, `components/`, `services/`.
8. Esegui una demo rapida (30–60 secondi) e annota cosa hai imparato.
9. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

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
