# Lab 06 — Esercitazione — Core vs third-party libraries; dependencies and versioning

## Obiettivo

- Applicare i micro-argomenti della lezione 06 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Devi aggiungere **una piccola feature di rete** (fetch di dati) e dimostrare di saper gestire **dipendenze e versioning** in modo disciplinato.

Scegli una di queste due opzioni (una sola):

- **Opzione A (core-only):** implementa la feature usando solo `fetch`.
- **Opzione B (third-party):** implementa la feature usando **Axios**.

In entrambi i casi devi documentare *perché* hai scelto quella strada.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Crea un piccolo servizio `services/api.js` con una funzione `fetchTodos(limit)` che legga da:

- `https://jsonplaceholder.typicode.com/todos?_limit=10`

1. Implementa una UI con **3 stati espliciti**: `loading`, `error`, `success`.
2. Gestisci **1 edge case** a scelta:

- rete offline / errore HTTP
- risposta vuota (0 elementi)

1. Se scegli l’**Opzione B (Axios)**:

- installa `axios` e verifica che siano stati aggiornati `package.json` e lockfile
- mostra l’albero dipendenze con `npm ls axios` (va bene anche solo in terminale)

Nota Expo:

- `axios` è una libreria **pure JS**, quindi `npm install axios` va bene.
- Per molte librerie con moduli nativi (camera, maps, ecc.), in Expo è spesso preferibile `npx expo install <pkg>` per avere versioni compatibili con l’SDK.

1. Documenta in `README.md` una sezione “Dependencies” con 3 righe:

- cosa hai aggiunto (o perché non hai aggiunto nulla)
- quale beneficio ottieni
- una nota su lockfile/versioning (1 frase)

1. Esegui una demo rapida (30–60 secondi).
2. Cleanup obbligatorio e verifica che il progetto riparta pulito.

## Reproducibility (bonus consigliato)

Se ti trovi con installazioni diverse tra macchine, prova:

```bash
npm ci
```

Regola: evitare “upgrade random” durante lo sviluppo della feature. Aggiorna una cosa per volta e verifica subito.

## Output atteso

- App eseguibile su emulatore o device
- UI chiara e leggibile
- Almeno un edge case gestito in modo esplicito
- `README.md` aggiornato con motivazione (core vs third-party)

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Lockfile presente e coerente
- [ ] Motivazione dipendenze scritta in `README.md`
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
