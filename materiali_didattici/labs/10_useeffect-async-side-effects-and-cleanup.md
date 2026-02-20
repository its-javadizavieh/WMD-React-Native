# Lab 10 — Esercitazione — useEffect; async side-effects and cleanup

## Obiettivo

- Applicare i micro-argomenti della lezione 10 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Devi costruire una schermata che carica dati in modo asincrono usando `useEffect`, gestendo correttamente **stati UI** e **cleanup**.

Tema suggerito: “Todos list” (da JSONPlaceholder).

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Implementa `useEffect` per caricare dati all’avvio (mount).
3. Gestisci **3 stati espliciti**:

    - `loading`
    - `error`
    - `success`

4. Aggiungi un pulsante “Reload” per rilanciare il caricamento.
5. Implementa **1 requisito di cleanup** (uno solo):

    - abort/cancellazione della richiesta (se possibile)
    - oppure cleanup di un `setInterval`/timer creato per demo

6. Gestisci **1 edge case**:

    - errore rete (mostra messaggio + retry)
    - risposta vuota

7. Demo rapida (30–60 secondi) spiegando *quando* si esegue l’effetto e *perché* il cleanup serve.
8. Cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- App eseguibile su emulatore o device
- UI chiara e leggibile
- Almeno un edge case gestito in modo esplicito
- useEffect usato correttamente (con stati e cleanup)

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Cleanup dell’effetto presente
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
