# Lab 02 — Esercitazione — Bridge architecture and native rendering (concepts, limitations)

## Obiettivo

- Applicare i micro-argomenti della lezione 02 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Costruisci una schermata con contatore e un componente figlio per osservare i re-render con `console.count`. Poi usa `FlatList` per mostrare una lista.

## Step (numerati)

1. Crea (o riusa) un progetto Expo e avvialo.
2. Implementa un contatore con `useState` e aggiungi `console.count` nei componenti.
3. Aggiungi un componente figlio che riceve una callback e osserva quando si ri-renderizza.
4. Implementa una lista usando `FlatList` con un `keyExtractor` stabile.
5. Scrivi 5 righe nel README del lab: cosa hai visto e perché succede.
6. Cleanup obbligatorio.

## Come tenere l'app veloce (regole semplici)

1) Evita lavoro pesante dentro il render (sort/filter di array grandi)
2) Dividi i componenti grandi in componenti più piccoli
3) Usa `FlatList` per liste lunghe
4) Tieni gli aggiornamenti di stato semplici

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

- react native rerender console.count
- react native performance rerender
- expo logs console.count
- flatlist keyextractor react native
