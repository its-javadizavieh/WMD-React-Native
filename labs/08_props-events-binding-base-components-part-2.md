# Lab 08 — Esercitazione — Props, events, binding; base components (Part 2)

## Obiettivo

- Applicare i micro-argomenti della lezione 08 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Devi costruire una mini UI “Settings” per esercitare **props, eventi (callback) e binding** usando componenti base (Part 2).

Obiettivo: ottenere componenti riutilizzabili con contratti chiari.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Crea un componente riutilizzabile `SettingRow` (o simile) con props:

    - `label: string`
    - `description?: string`
    - `right: ReactNode` (o un’alternativa equivalente)

3. Nella schermata principale, crea 2 righe impostazioni:

    - una con `TextInput` (binding con `value` + `onChangeText`)
    - una con `Switch` (binding con `value` + `onValueChange`)

4. Definisci **eventi chiari**: i componenti figli non devono “decidere” cosa fare, ma chiamare callback.
5. Gestisci **1 edge case**:

    - input vuoto → messaggio o stato “non valido”
    - input con soli spazi → trim

6. Demo rapida: spiega in 3 frasi “data down, events up”.
7. Cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- App eseguibile su emulatore o device
- UI chiara e leggibile
- Almeno un edge case gestito in modo esplicito
- Almeno 1 componente riutilizzabile con props ben definite

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Props ed eventi (callback) coerenti e leggibili
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
