# Lab 05 — Esercitazione — Modular architecture in React Native (modules, components, screens)

## Obiettivo

- Applicare i micro-argomenti della lezione 05 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Prendi una mini-app funzionante (anche quella dei lab precedenti) e **refactorala** per rispettare una struttura modulare chiara.

Obiettivo: a fine lab, il progetto deve avere separazione minima tra **screens**, **components** e **services** e una direzione di dipendenze sensata.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Crea le cartelle: `screens/`, `components/`, `services/`.
3. Estrai **almeno 1 componente** riusabile in `components/` (nessun cambio di comportamento).
4. Sposta **almeno 1 side effect** in `services/` (es. accesso dati, wrapper di API, helper con stato).
5. Crea/usa **una screen** in `screens/` che orchestri stato + chiamate a `services/` e passi props ai componenti.
6. Verifica la direzione dipendenze (regola semplice): `screens → components/services`, `services` non importa UI.
    - Regola facile (bonus): components importano solo components/utils; services importano solo services/utils.
7. Gestisci **almeno un edge case** con messaggio chiaro (es. input vuoto, lista vuota, errore).
8. Esegui una demo rapida (30–60 secondi) e annota cosa hai imparato.
9. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

## Bonus (se il progetto cresce): “public API” del modulo

Per evitare import profondi, puoi esportare da un solo punto:

```js
// features/notes/index.js
export { NotesScreen } from './screens/NotesScreen';
export { addNote, listNotes } from './services/notes';
```

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
