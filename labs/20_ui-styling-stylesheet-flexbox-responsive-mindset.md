# Lab 20 — Esercitazione — UI styling: StyleSheet + Flexbox + responsive mindset

## Obiettivo

- Applicare i micro-argomenti della lezione 20 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Realizza una schermata UI con layout Flexbox e styling tramite StyleSheet, che si adatta a schermi diversi (narrow vs wide / portrait vs landscape).

## Step (numerati)

1. Crea una schermata con:

   - header (titolo + descrizione breve)
   - contenuto (lista di card o griglia semplice)

1. Usa StyleSheet (no stile “sparso” ovunque):

   - stili riutilizzabili
   - composizione con array di stili quando serve

1. Usa Flexbox in modo intenzionale:

   - `flexDirection`, `justifyContent`, `alignItems`
   - spaziature coerenti (padding/margin)

1. Responsive obbligatorio:

   - cambia layout in base a larghezza/orientamento (narrow vs wide)

1. Edge case obbligatorio: gestisci testo lungo o device piccolo senza “tagli brutti” (layout ancora leggibile).
1. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- UI chiara e leggibile con StyleSheet + Flexbox
- Due layout diversi (narrow vs wide)
- Edge case gestito: leggibilità anche con contenuti lunghi/piccoli schermi

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
