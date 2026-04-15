# Lab 13 – React Navigation: setup e concetti base

## Obiettivo

- Setup `NavigationContainer` + `createNativeStackNavigator`.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Setup `NavigationContainer` + `createNativeStackNavigator`. Due screen: Home → Details con navigazione.

> **Perché questo lab:** esercitare i pattern della lezione 13 in una mini-app concreta.

## Cosa imparerai

1. Come installare React Navigation con Expo.
2. Come creare un `Stack.Navigator` con due screen.
3. Come navigare con `navigation.navigate("Details", { id: "a1" })`.
4. Come tornare indietro con `navigation.goBack()`.

## Dipendenze (Expo)

```bash
npx expo install @react-navigation/native @react-navigation/native-stack react-native-screens react-native-safe-area-context
```

## Passi

1. **Installa dipendenze** — Esegui i comandi di installazione sopra.
2. **App.tsx** — Crea `NavigationContainer` con `Stack.Navigator` e due screen: Home e Details.
3. **HomeScreen** — Un pulsante che naviga a Details con `navigation.navigate("Details", { id: "a1" })`.
4. **DetailsScreen** — Mostra l'id ricevuto e un pulsante "Go back".
5. **Edge case** — Se `route.params?.id` è mancante, mostra "Missing id".

## Screenshot attesi

**Home**

![Lab 13 - Home](imgs/lab_13_home.png)

**Details**

![Lab 13 - Details](imgs/lab_13_details.png)


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

- react navigation expo setup
stack navigator react native
navigation.navigate params
