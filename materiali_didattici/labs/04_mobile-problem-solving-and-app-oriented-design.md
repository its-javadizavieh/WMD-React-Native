# Lab 04 — Esercitazione — Mobile problem solving and app-oriented design

## Obiettivo

- Applicare i micro-argomenti della lezione 04 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Realizza una piccola feature coerente con i micro-argomenti della lezione (problem solving + design app-oriented). L’obiettivo è consegnare una soluzione verificabile: **flow chiaro**, **stati espliciti**, **1 edge case gestito**.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Scrivi prima di tutto (nel README del progetto o in fondo al lab) una requirement in 1 frase: “L’utente può … così che …”.
3. Definisci gli stati della feature/schermata: **empty / loading / success / error** (anche solo a testo).
4. Implementa la feature in modo minimale seguendo gli stati definiti.
5. Aggiungi gestione di **almeno un edge case** (es. input vuoto, lista vuota, errore rete, permesso negato) con messaggio chiaro.
    - Regola: lo stato “error” deve essere **actionable** (es. retry o next step).
6. (Facoltativo se utile) Organizza in moduli: `screens/`, `components/`, `services/`.
7. Esegui una demo rapida (30–60 secondi) e annota cosa hai imparato.
8. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Manual test checklist (obbligatoria)

Prima della consegna, forza intenzionalmente questi stati:

- Loading: inserisci un `setTimeout` o una `await` finta per vedere il loader
- Empty: ritorna una lista vuota dal servizio
- Error: fai `throw new Error()` nel servizio e verifica UI + messaggio
- Success: ritorna dati validi

Se non riesci a mostrare uno stato, il flow non è completo.

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
