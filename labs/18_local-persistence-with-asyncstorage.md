# Lab 18 – Gestione locale: AsyncStorage

## Obiettivo

- Load / save / reset con `AsyncStorage`.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Load / save / reset con `AsyncStorage`. Persistenza automatica su cambio.

> **Perché questo lab:** esercitare i pattern della lezione 18 in una mini-app concreta.

## Cosa imparerai

1. Come installare `@react-native-async-storage/async-storage`.
2. Come usare `getItem`, `setItem`, `removeItem`.
3. Come caricare dati al mount con `useEffect`.
4. Come persistere automaticamente quando lo stato cambia.

## Dipendenze (Expo)

```bash
npx expo install @react-native-async-storage/async-storage
```

## Passi

1. **Installa** — `npx expo install @react-native-async-storage/async-storage`.
2. **Load al mount** — `AsyncStorage.getItem(KEY)` in un `useEffect`.
3. **Save automatico** — `AsyncStorage.setItem(KEY, text)` in un secondo `useEffect` che dipende da `text`.
4. **Reset** — Pulsante che chiama `AsyncStorage.removeItem(KEY)`.
5. **Edge case** — Valore assente → mostra "(empty)".

## Screenshot attesi

**Preferences**

![Lab 18 - Preferences](imgs/lab_18_main.png)


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

- asyncstorage react native
expo install asyncstorage
local storage react native
