# Lab 15 — Esercitazione — Advanced navigation and deep linking

## Obiettivo

- Applicare i micro-argomenti della lezione 15 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Estendi una mini-app con navigazione aggiungendo un **deep link** che apre direttamente una schermata di dettaglio.

Esempio target:

- `myapp://details/:id` → apre `Details` con param `id`

Nota: il deep link è input non affidabile → serve validazione e fallback UI.

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
1. Crea (o riusa) uno stack con `Home` e `Details`.
1. Configura il `linking` in `NavigationContainer`:

    - prefix (es. `myapp://`)
    - mapping route (es. `details/:id`)

1. Testa il deep link con `npx uri-scheme open "myapp://details/a1" --android`.
1. In `Details`, valida `route.params?.id` e gestisci almeno questi casi:

    - id mancante/invalid → UI di errore + Back
    - id non trovato → UI “Not found” + Back

1. Se vuoi, aggiungi una nota su back behavior (perché la UX deve essere prevedibile).
1. Se utile, organizza in moduli: `screens/`, `components/`, `services/`.
1. Esegui una demo rapida (30–60 secondi) e annota cosa hai imparato.
1. Esegui il cleanup obbligatorio e verifica che il progetto riparta pulito.

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
