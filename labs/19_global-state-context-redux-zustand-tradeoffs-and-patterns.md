# Lab 19 – Stato globale: Context / Redux / Zustand

## Obiettivo

- Context + Provider con `useState`.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Context + Provider con `useState`. Hook custom per consumare il contesto. Toggle tema light/dark.

> **Perché questo lab:** esercitare i pattern della lezione 19 in una mini-app concreta.

## Cosa imparerai

1. Come creare un Context con `React.createContext`.
2. Come creare un Provider che wrappa l'app.
3. Come consumare il contesto con `React.useContext`.
4. Il pattern theme toggle: light ↔ dark.

## Passi

1. **Avvia progetto** — verifica che l'app parta.
2. **ThemeContext** — `React.createContext({ theme: "light", toggleTheme: () => {} })`.
3. **ThemeProvider** — Usa `useState("light")` e una funzione `toggleTheme`.
4. **Screen** — Usa `React.useContext(ThemeContext)` per leggere il tema e mostrare un toggle.
5. **App.tsx** — Wrappa `<Screen />` con `<ThemeProvider>`.
6. **Edge case** — Cambia lo sfondo in base al tema (light → bianco, dark → #333).

## Screenshot attesi

**Tema light — Context + Provider con useState**

![Lab 19 – Tema light](imgs/lab_19_light.png)

**Tema dark — toggle con useContext**

![Lab 19 – Tema dark](imgs/lab_19_dark.png)


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

- react context provider usecontext
react native theme toggle
creatcontext react native
