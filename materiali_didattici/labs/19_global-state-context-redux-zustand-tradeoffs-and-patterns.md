# Lab 19 — Esercitazione — Global state: Context / Redux / Zustand (tradeoffs and patterns)

## Obiettivo

- Applicare i micro-argomenti della lezione 19 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Implementa una feature che richiede stato condiviso tra *almeno due* schermate.

Scegli UNO scenario:

- “Preferiti”: aggiungi/rimuovi un item dai preferiti in una schermata e visualizzalo in un’altra
- “Theme toggle”: cambia un’impostazione globale e usala in due schermate

## Step (numerati)

1. Avvia l’app e verifica navigazione/2 schermate (o crea due schermate).
1. Implementa uno stato globale con Context + reducer:

- stato minimo (es. `favorites: string[]` oppure `theme: 'light' | 'dark'`)
- azioni minime (add/remove o toggle)

1. Consuma lo stato in due schermate:

- una schermata aggiorna lo stato
- una schermata legge e mostra lo stato

1. Edge case obbligatorio: gestisci uno stato vuoto (es. “nessun preferito”).
1. (Bonus, 5 minuti) Scrivi 3 righe di riflessione: perché qui basta Context? quando preferiresti Zustand/Redux?
1. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- Stato globale aggiornabile e visibile in più schermate
- Edge case gestito: stato vuoto con messaggio chiaro

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
