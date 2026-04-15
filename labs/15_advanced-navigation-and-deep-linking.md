# Lab 15 – Navigazione avanzata e deep linking

## Obiettivo

- Configurazione deep linking con `linking` object.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Configurazione deep linking con `linking` object. Validazione parametro da URL. Test con `npx uri-scheme open`.

> **Perché questo lab:** esercitare i pattern della lezione 15 in una mini-app concreta.

## Cosa imparerai

1. Come creare un `linking` config con `prefixes` e `config.screens`.
2. Come testare deep link con `npx uri-scheme open`.
3. Come validare parametri ricevuti da deep link.
4. Perché i parametri da URL sono "unreliable input".

## Passi

1. **Installa dipendenze** — React Navigation (se non già presente).
2. **App.tsx** — Aggiungi `linking` object con `prefixes: ["myapp://"]` e mappa delle screen.
3. **HomeScreen** — Pulsante che naviga a Details + testo che mostra il deep link path.
4. **DetailsScreen** — Legge `route.params?.id`. Se manca → "Invalid deep link".
5. **Test** — Esegui `npx uri-scheme open "myapp://details/a1" --android` nel terminale.

## Screenshot attesi

**Home con deep link — configurazione prefixes e screens**

![Lab 15 – Home con deep link](imgs/lab_15_home.png)

**Details via deep link — apertura diretta con URL**

![Lab 15 – Details via deep link](imgs/lab_15_details.png)


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

- react navigation deep linking
npx uri-scheme open
expo deep link config
