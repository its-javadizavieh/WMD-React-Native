# Lab 18 — Esercitazione — Local persistence with AsyncStorage

## Obiettivo

- Applicare i micro-argomenti della lezione 18 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Implementa una piccola preferenza utente o feature che rimane salvata tra riavvii dell’app usando AsyncStorage.

Esempi (scegline UNO):

- toggle “dark mode” (solo come stato, non serve un tema completo)
- lista “preferiti” (id salvati)
- ultimo testo di ricerca salvato

## Step (numerati)

1. Avvia l’app e implementa la feature scelta (stato + UI).
2. Crea un piccolo wrapper (es. `storage/` o `services/`) per leggere/scrivere su AsyncStorage.
3. Salva il valore quando cambia.
4. All’avvio della schermata/app, carica il valore e inizializza lo stato.
5. Edge case obbligatorio: gestisci JSON non valido (try/catch + reset a default).
6. Aggiungi un pulsante “Reset” che pulisce il valore salvato.
7. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- Valore persistito e ripristinato dopo riavvio
- Reset funzionante
- Edge case gestito: JSON corrotto non manda in crash

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
