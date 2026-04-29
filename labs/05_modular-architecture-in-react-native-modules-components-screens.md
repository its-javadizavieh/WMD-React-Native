# Lab 05 - Architettura modulare in React Native

## Obiettivo

- Prendi l'app Notes del lab 04 e modularizzala senza cambiare nulla della feature.
- Spezza il codice in `screens/`, `components/` e `services/`.
- Estrai `PrimaryButton` come componente riusabile e `notes`/`addMessage` come service separato.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Il lab 05 **non è un esercizio nuovo**: è il lab 04 spezzato in moduli. Parti dalla tua soluzione Notes e distribuiscila su più file senza toccare nessun comportamento.

> **Perché questo lab:** dopo il lab 04 hai una schermata funzionante ma tutto in `App.tsx`. In un progetto reale questo diventa illeggibile in pochi giorni. Separare ora screens, components e services è il primo passo verso un'architettura mantenibile.

## Cosa imparerai

1. Come distribuire il codice del lab 04 tra `screens/`, `components/` e `services/`.
2. La regola degli import: screens possono importare components e services, mai il contrario.
3. Come estrarre un bottone riusabile con `interface` per le props.
4. Come spostare dati e logica in un service dedicato.
5. Come lasciare `App.tsx` ridotto al minimo.

## File da creare

```text
services/users.ts
components/PrimaryButton.tsx
screens/UsersScreen.tsx
App.tsx
```

## Starter pattern (solo promemoria)

```tsx
// App.tsx - deve restare così semplice
import UsersScreen from "./screens/UsersScreen";

export default function App() {
  return <UsersScreen />;
}
```

## Passi

1. **Riparti dal lab 04** - usa la tua soluzione Notes già funzionante, non creare una nuova app.
2. **Crea le cartelle** - `screens/`, `components/`, `services/`.
3. **Estrai il service** - sposta `notes` e `addMessage()` in `services/users.ts` ed esportali.
4. **Estrai il bottone** - crea `components/PrimaryButton.tsx` con `interface PrimaryButtonProps` (`label` e `onPress`); rimuovi il `Pressable` inline dalla screen.
5. **Crea la screen** - sposta tutta la UI in `screens/UsersScreen.tsx`: `TextInput`, stato, `load()`, `onAdd()`, lista note e messaggi di fallback.
6. **Semplifica App.tsx** - importa e renderizza soltanto `<UsersScreen />`.
7. **Non cambiare la feature** - il risultato finale deve comportarsi esattamente come il lab 04.
8. **Verifica gli import** - screen → components + services; services non importano UI.
9. **Edge case già presenti** - testo vuoto ignorato, stato `empty` con messaggio, stessa UX del lab precedente.

## Screenshot attesi

**Stesso stato empty del lab 04, ma con codice separato**

![Lab 05 - Stato empty](imgs/lab_04_empty.png)

**Una nota aggiunta dopo il refactor modulare**

![Lab 05 - Una nota aggiunta](imgs/lab_04_success_1.png)

**Struttura cartelle - components / screens / services**

![Lab 05 - Struttura cartelle](imgs/lab_05_structure.png)

## Consegna minima

- App che parte su emulatore o device
- Stessa feature del lab 04, ma distribuita su più file
- Almeno un componente riusabile e un service separato

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Lab 04 funziona ancora identicamente
- [ ] Codice separato in `screens/`, `components/`, `services/`
- [ ] Cleanup completato

## Problemi comuni

- Se un import non si risolve: controlla i percorsi relativi (`../components/...`, `../services/...`).
- Se il pulsante non funziona: verifica che `label` e `onPress` siano passati correttamente.
- Se la lista non si aggiorna: assicurati che `load()` venga richiamata dopo `addMessage()`.

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall'OS.
- Se hai usato storage locale: svuota i dati dell'app o rimuovi le chiavi salvate.

## Search terms

- react native modular architecture
- react native extract component props
- react native screens components services
