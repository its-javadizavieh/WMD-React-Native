# Lab 14 - Navigazione avanzata e deep linking

## Obiettivo

- Parti dalla stessa app del **Lab 13** (stack navigation + `FlatList` + route params).
- Aggiungi configurazione deep linking con `linking` object.
- Gestisci almeno un edge case con un messaggio chiaro (stessi messaggi del Lab 13).

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale
- **Lab 13 completato** (stessa app con stack navigation e route params)

> **Riferimento completo deep linking:** Cheat Sheet → [§26 - Deep linking](00_cheatsheet_react-native-programming_en.md#26--deep-linking) (`00_cheatsheet_react-native-programming_en.md`). Include URL `exp://`, due terminali, errori comuni e screenshot.

## Due terminali - emulatore + Metro + deep link

Per questo lab servono **due terminali** aperti insieme. Metro **blocca** il terminale: non lanciare `expo start` e `uri-scheme open` nello stesso terminale.

| Terminale                    | Cosa fai                                                                                                                                                                           |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1 - Emulatore e test URL** | Avvia l'AVD da Android Studio (**Virtual Device Manager** → ▶). Verifica `adb devices`. Quando l'app è in esecuzione in **Expo Go**, lancia qui il deep link (vedi comando sotto). |
| **2 - Progetto (Metro)**     | `cd MyFirstApp` → `npx expo start` → premi **`a`** e attendi la **Home** sull'emulatore. **Lascia questo terminale aperto.**                                                       |

### Comando di test (Expo Go - emulatore Android)

Con Metro ancora in esecuzione nel **terminale 2**:

```bash
npx uri-scheme open "exp://10.0.2.2:8081/--/details/a1" --android
```

- **`10.0.2.2`** = IP del tuo PC visto dall'emulatore Android (non usare `127.0.0.1`).
- Su **telefono fisico** (stessa Wi‑Fi): sostituisci con l'IP del PC che vedi nel terminale Metro (es. `exp://192.168.1.6:8081/--/details/a1`).
- Il path deve essere **`details/a1`** (inglese) - non `dettagli/a1`.

> **`myapp://details/a1` non funziona con Expo Go** - solo con dev build (`npx expo run:android`). Per il corso usiamo **`exp://...`**. Dettagli, tabelle HOST e troubleshooting: [Cheat Sheet §26](00_cheatsheet_react-native-programming_en.md#26--deep-linking).

Ordine consigliato:

1. Terminale 1 → emulatore acceso, `adb devices` ok
2. Terminale 2 → `npx expo start` → premi `a` → Home visibile in Expo Go
3. Terminale 1 → comando `exp://10.0.2.2:8081/--/details/a1` → Details con `id: a1`

Se Expo non trova il device: terminale 1, `adb devices` - se vuoto, riavvia l'emulatore.

## Scenario

Riprendi l'app del Lab 13 (lista items → dettaglio con `id` validato) e aggiungi deep linking: l'URL `details/a1` apre direttamente Details con lo stesso `route.params.id` usato dalla navigazione normale.

> **Perché questo lab:** esercitare i pattern della lezione 14 sulla stessa mini-app del Lab 13, aggiungendo solo il layer di deep linking.

## Cosa imparerai

1. Come estendere un'app con stack navigation già funzionante con un `linking` config (`prefixes` + `config.screens`).
2. Come testare deep link con `npx uri-scheme open` e URL **`exp://`** su Expo Go (opzionale: test web nel browser).
3. Come i parametri da URL finiscono in `route.params` — stessa validazione del Lab 13.
4. Perché i parametri da URL sono "unreliable input".

## Passi

1. **Parti dal Lab 13** - Copia (o riusa) `App.tsx`, `HomeScreen` e `DetailsScreen` con `FlatList`, navigazione e validazione `id` / item non trovato.
2. **Installa dipendenze** - `npx expo install expo-linking` (React Navigation già presente dal Lab 13).
3. **app.json** - Aggiungi `"scheme": "myapp"` sotto `expo` (per dev build con `myapp://`).
4. **App.tsx** - Aggiungi `linking` con `prefixes: [Linking.createURL("/"), "myapp://"]`, passa `linking={linking}` a `NavigationContainer`, mappa `Details: "details/:id"`.
5. **HomeScreen** - Mantieni la `FlatList` del Lab 13; aggiungi in fondo un testo con esempio URL `exp://...` per il test deep link.
6. **DetailsScreen** - Nessuna modifica alla logica: `route.params?.id` funziona sia da tap in lista sia da deep link. Edge case: id mancante → "Invalid route param"; item non trovato → "Product not found".
7. **Test mobile** - Terminale 2: Metro + app aperta su Home. Terminale 1: `npx uri-scheme open "exp://10.0.2.2:8081/--/details/a1" --android` → Details con Alpha.
8. **(Opzionale) Test web** - `npx expo start --web` → nel browser: `http://localhost:8081/details/a1` (nessun `uri-scheme`, nessun `/--/`). Vedi [Cheat Sheet §26](00_cheatsheet_react-native-programming_en.md#26--deep-linking).

## Screenshot attesi

**Lista items - FlatList con navigazione a dettaglio**

![Lab 13 - Lista items](imgs/lab_13_list.png)

**Dettaglio item - parametro id passato via route params**

![Lab 13 - Dettaglio item](imgs/lab_13_details_1.png)
![Lab 13 - Dettaglio item](imgs/lab_13_details_2.png)
![Lab 13 - Dettaglio item](imgs/lab_13_details_3.png)

## Consegna minima

- App che parte su emulatore o device
- Lista → dettaglio funziona come nel Lab 13
- Deep link `details/a1` apre Details con item corretto
- Edge case gestiti: id mancante e item non trovato

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Home → Details → Back funziona (tap in lista)
- [ ] Deep link `exp://.../details/a1` apre Details con Alpha
- [ ] Edge case gestito con messaggio chiaro (es. `details` senza id, o id inesistente)
- [ ] Cleanup completato

## Problemi comuni

Vedi [Cheat Sheet §26 - Deep linking](00_cheatsheet_react-native-programming_en.md#26--deep-linking) (screenshot e troubleshooting inclusi).

- **`unable to resolve Intent` con `myapp://`** - stai usando Expo Go: passa a `exp://10.0.2.2:8081/--/details/a1`.
- **Schermata blu "Something went wrong"** - Metro non avviato, app non aperta prima su Home, o IP sbagliato (`10.0.2.2` su emulatore).
- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l'emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall'OS.
- Se hai usato storage locale: svuota i dati dell'app o rimuovi le chiavi salvate.

## Search terms

- react navigation deep linking
- npx uri-scheme open exp://
- expo linking createURL
- expo deep link config
