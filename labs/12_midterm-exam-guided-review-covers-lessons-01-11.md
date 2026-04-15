# Lab 12 – Verifica intermedia e riepilogo guidato (Lezioni 01-11)

## Obiettivo

- Riepilogo dei pattern principali: UiState, load(), retry.
- Dimostra di saper costruire una schermata con stati espliciti.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

4h (verifica + revisione)

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Costruisci una schermata che usa il pattern UiState completo: loading / empty / error / success. È un ripasso di tutti i concetti visti nelle lezioni 01-11.

> **Perché questo lab:** è il punto di verifica. Se riesci a costruire questa schermata da zero, hai solidità sulle basi.

## Cosa ripasserai

1. `useState` con `status` string per gli stati.
2. Una funzione `load()` che gestisce loading → success/error.
3. UI condizionale per ogni stato.
4. `useEffect` per il caricamento iniziale.

## Starter pattern (solo promemoria)

```tsx
function load() {
  setStatus("loading");
  setTimeout(() => {
    setStatus("success");
  }, 800);
}

<Pressable onPress={load}>
  <Text>Riprova</Text>
</Pressable>
```

## Passi

1. **Avvia progetto** — da zero o riusando un lab precedente.
2. **Definisci stati** — idle / loading / empty / error / success.
3. **Funzione load()** — Simula un fetch con `setTimeout`.
4. **UI per ogni stato** — Un `if` per ciascuno.
5. **Pulsante Riprova** — Richiama `load()`.
6. **Cleanup e consegna.**

## Screenshot attesi

**Midterm review**

![Lab 12 - Midterm review](imgs/lab_12_main.png)


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

- react native usestate loading pattern
- react native screen states
