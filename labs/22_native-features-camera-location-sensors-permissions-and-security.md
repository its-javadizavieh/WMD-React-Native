# Lab 22 – Funzionalità native: posizione, permessi e sicurezza

## Obiettivo

- Flusso permission-first: richiedi permesso → leggi dato.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Flusso permission-first: richiedi permesso → leggi dato. Fallback se negato con link a Settings.

> **Perché questo lab:** esercitare i pattern della lezione 22 in una mini-app concreta.

## Cosa imparerai

1. Come installare `expo-location`.
2. Come richiedere un permesso con `requestForegroundPermissionsAsync`.
3. Come gestire il rifiuto del permesso con UI fallback.
4. Come aprire le Settings del device con `Linking.openSettings()`.

## Dipendenze (Expo)

```bash
npx expo install expo-location
```

## Passi

1. **Installa** — `npx expo install expo-location`.
2. **Funzione askLocation()** — Richiede permesso e ritorna "granted" o "denied".
3. **UI per ogni stato** — unknown / denied / granted con lat/lng.
4. **Fallback su denied** — Pulsante "Open Settings" che chiama `Linking.openSettings()`.
5. **Edge case** — Nega il permesso e verifica che l'app resta usabile.

## Screenshot attesi

**Permesso richiesto — flusso permission-first, UI per stato unknown/denied**

![Lab 22 – Permesso richiesto](imgs/lab_22_permission.png)

**Location ottenuta — coordinate mostrate dopo permesso granted**

![Lab 22 – Location ottenuta](imgs/lab_22_location.png)


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

- expo-location permissions
react native linking openSettings
expo install expo-location
