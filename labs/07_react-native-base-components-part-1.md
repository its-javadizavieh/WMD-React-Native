# Lab 07 — Esercitazione — React Native base components (Part 1)

## Obiettivo

- Applicare i micro-argomenti della lezione 07 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Devi realizzare una **schermata statica ma curata** usando solo i componenti base (Part 1) e una struttura leggibile.

Tema suggerito: “Profile + Highlights”.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
2. Implementa una schermata che contenga **almeno**:

    - una sezione header con `Image` + `Text`
    - una card (anche semplice) con contenuti testuali
    - un’area interattiva con `Pressable` (anche solo per loggare/mostrare un messaggio)

3. Usa `ScrollView` se la schermata può andare in overflow (anche solo per abitudine corretta).
4. Gestisci **1 edge case** legato ai componenti base:

    - immagine mancante → fallback (iniziali o placeholder)
    - testo troppo lungo → layout ancora leggibile

5. Mantieni lo stile semplice ma coerente: spaziature costanti, allineamenti chiari.
6. Demo rapida (30–60 secondi) spiegando le scelte di layout.
7. Cleanup obbligatorio e verifica che il progetto riparta pulito.

## Output atteso

- App eseguibile su emulatore o device
- UI chiara e leggibile
- Almeno un edge case gestito in modo esplicito

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Uso corretto di `View`/`Text`/`Image`/`Pressable`
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
