# Lab 22 — Esercitazione — Native features: camera/location/sensors; permissions and security

## Obiettivo

- Applicare i micro-argomenti della lezione 22 in una consegna pratica.
- Produrre una funzionalità dimostrabile con gestione errori/edge case.

## Durata (timebox)

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo (consigliato per il corso) oppure React Native CLI (solo Android)
- Android emulator *oppure* telefono reale (consigliato)

## Scenario

Implementa **UNA** feature che usa una capacità nativa:

- camera **oppure** location **oppure** un sensore

La feature deve avere una UX “permission-first”:

- richiedi il permesso solo dopo un’azione utente
- gestisci denial e “non disponibile” senza crash
- spiega in UI perché la permission serve (privacy/security mindset)

## Step (numerati)

1. Avvia (o crea) un progetto Expo e verifica che l’app parta su emulatore/device.
1. Scegli una capability (camera/location/sensori) e installa **solo** il package necessario (Expo workflow).
1. Implementa una UI con un bottone “Start/Request” che:

    - chiede permesso (just-in-time)
    - se granted, esegue l’azione (es. legge posizione / apre camera)

1. Modella stati espliciti (esempio): `idle/requesting/denied/error/success`.
1. Edge case obbligatorio (scegline almeno uno e rendilo dimostrabile):

    - permesso negato
    - feature non disponibile su emulatore/device
    - errore runtime (try/catch + messaggio)

1. (Bonus) Aggiungi un’azione “Apri impostazioni” quando la permission è negata.
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
