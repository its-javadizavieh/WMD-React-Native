# Lab 11 — Esercitazione — Forms in mobile: controlled forms and patterns

## Obiettivo

- Applicare i micro-argomenti della lezione 11 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Devi costruire una piccola schermata con **form controllato** (es. “Sign up” o “Login”) per esercitare:

- `value` + `onChangeText` (controlled inputs)
- validazione semplice (con pattern `touched` o `submitted`)
- stati di submit (`idle/loading/error/success`)

Obiettivo: form prevedibile + feedback chiaro + niente comportamenti “random”.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Implementa un form con almeno 2 campi (es. email + password; o name + email + password).
3. Rendi i campi controllati:

    - ogni input ha `value`
    - ogni input aggiorna lo stato con `onChangeText`

4. Aggiungi una validazione minima (es. email contiene `@`, password >= 6).
5. Applica un pattern per *quando* mostrare gli errori:

    - `touched` su `onBlur` **oppure**
    - `submitted` al primo submit

6. Implementa stati di submit:

    - `loading` mentre invii
    - `error` con messaggio chiaro su fallimento
    - `success` con conferma

7. Gestisci 1 edge case (es. submit mentre non valido / doppio tap / errore rete simulato).
8. Cleanup obbligatorio e verifica che il progetto riparta pulito.

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
