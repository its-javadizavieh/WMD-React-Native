# Lab 23 – Notifiche, background task ed esame finale

## Obiettivo

- Scheduling notifica locale con `expo-notifications`.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Scheduling notifica locale con `expo-notifications`. Flusso permessi e gestione rifiuto. Esame finale.

> **Perché questo lab:** esercitare i pattern della lezione 23 in una mini-app concreta.

## Cosa imparerai

1. Come installare `expo-notifications`.
2. Come richiedere permesso notifiche.
3. Come schedulare una notifica locale con timer.
4. Come gestire il rifiuto permesso con fallback UI.

## Dipendenze (Expo)

```bash
npx expo install expo-notifications
```

## Passi

1. **Installa** — `npx expo install expo-notifications`.
2. **setNotificationHandler** — Config per mostrare alert su notifica ricevuta.
3. **Funzione schedule()** — Richiede permesso, poi schedula una notifica a 5 secondi.
4. **UI per ogni stato** — idle / denied / scheduled.
5. **Edge case** — Nega il permesso e verifica il messaggio.
6. **Esame finale** — Questa è anche la struttura per il mini-progetto individuale.

## Screenshot attesi

**Notifica schedulata — scheduling con permessi e UI per ogni stato**

![Lab 23 – Notifica schedulata](imgs/lab_23_main.png)


## Consegna minima

- App che parte su emulatore o device
- UI chiara e leggibile
- Un edge case gestito con un messaggio chiaro

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Cleanup completato

## Problemi comuni

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l'emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.
- Se l'app non si connette: controlla che PC e device siano sulla stessa rete (LAN).

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall'OS.
- Se hai usato storage locale: svuota i dati dell'app o rimuovi le chiavi salvate.

## Search terms

- expo-notifications schedule
expo install expo-notifications
react native local notification
