# Lab 21 — Esercitazione — Themes/UI kit; accessibility + scaling; basic animations

## Obiettivo

- Applicare i micro-argomenti della lezione 21 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Costruisci una mini “UI kit demo” composta da:

- **theme tokens** (almeno spacing + typography + radius)
- **2–3 primitive riutilizzabili** (es. `Card`, `PrimaryButton`, `Title`)
- **1 miglioramento accessibilità/scaling** verificabile
- **1 animazione base** (feedback su press, expand, ecc.)

Obiettivo: una schermata che mostra coerenza visiva, leggibilità e feedback (non una palette o design system completo).

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
1. Crea un file di theme tokens (es. `src/ui/theme.js`) con:

    - `spacing` (pochi valori)
    - `typography` (2–3 size)
    - `radius`

1. Crea 2–3 primitive riutilizzabili (es. `Card`, `PrimaryButton`) che usano i tokens.
1. Costruisci una schermata demo usando *solo* quelle primitive (no duplicazioni inutili).
1. Accessibilità/scaling obbligatorio:

    - aggiungi `accessibilityRole`/`accessibilityLabel` dove serve
    - verifica font scaling / testo lungo: il layout resta leggibile (wrap, no overflow)

1. Animazione base obbligatoria:

    - feedback su press (scale/opacity) oppure piccola transizione

1. Edge case obbligatorio: testo lungo + font grandi → UI ancora leggibile.
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
