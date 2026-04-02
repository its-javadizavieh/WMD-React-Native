# Guida - Collegamento dispositivi Android e iPhone

> Questa guida spiega come collegare il tuo telefono (Android o iPhone) al progetto Expo per testare l'app direttamente sul dispositivo.

---

## Prerequisiti

- Node.js installato sul computer
- Progetto Expo creato (`npx create-expo-app my-app --template blank-typescript`)
- Telefono e computer collegati alla **stessa rete Wi-Fi**

---

## 1. Installare Expo Go sul telefono

| Piattaforma | Store             | Link            |
| ----------- | ----------------- | --------------- |
| **Android** | Google Play Store | Cerca "Expo Go" |
| **iPhone**  | Apple App Store   | Cerca "Expo Go" |

---

## 2. Avviare il progetto

```bash
cd my-app
npx expo start
```

Nel terminale apparirà un **QR code**. Questo serve per collegare il telefono.

---

## 3. Collegamento Android

### 3.1 Scansiona il QR code

1. Apri l'app **Expo Go** sul telefono Android
2. Tocca **"Scan QR Code"**
3. Inquadra il QR code nel terminale
4. L'app si carica automaticamente

### 3.2 Se il QR code non funziona (rete bloccata)

Alcuni Wi-Fi scolastici o aziendali bloccano la comunicazione tra dispositivi. In questo caso:

```bash
# Usa il tunnel (più lento ma funziona sempre)
npx expo start --tunnel
```

Se richiesto, installa `@expo/ngrok`:

```bash
npx expo install @expo/ngrok@^4.1.0
```

### 3.3 Attivare il debug USB (opzionale - per emulatore o cavo)

Se vuoi collegare il telefono Android via **cavo USB**:

1. **Abilita le Opzioni sviluppatore:**
   - Vai in **Impostazioni → Info sul telefono**
   - Tocca **"Numero build"** 7 volte di seguito
   - Apparirà il messaggio: "Ora sei uno sviluppatore"

2. **Abilita il Debug USB:**
   - Vai in **Impostazioni → Opzioni sviluppatore**
   - Attiva **"Debug USB"**

3. **Collega il cavo USB** e accetta il prompt "Consenti debug USB?" sul telefono

4. **Verifica la connessione:**

   ```bash
   adb devices
   ```

   Dovresti vedere il tuo dispositivo nella lista.

5. **Avvia su dispositivo:**
   ```bash
   npx expo start
   # Premi 'a' nel terminale per aprire su Android
   ```

### 3.4 Usare l'emulatore Android (senza telefono fisico)

1. Installa **Android Studio** → apri **Virtual Device Manager**
2. Crea un dispositivo (es. Pixel 7, API 34)
3. Avvia l'emulatore
4. Nel terminale Expo, premi **`a`** per aprire l'app nell'emulatore

---

## 4. Collegamento iPhone

### 4.1 Scansiona il QR code

1. Apri la **Fotocamera** dell'iPhone (non serve Expo Go per scansionare)
2. Inquadra il QR code nel terminale
3. Tocca la notifica **"Apri in Expo Go"**
4. L'app si carica automaticamente

### 4.2 Se il QR code non funziona

```bash
npx expo start --tunnel
```

### 4.3 Limitazioni iPhone

| Aspetto            | Dettaglio                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------- |
| **Expo Go**        | Funziona per lo sviluppo, ma alcune librerie native (es. notifiche push reali) richiedono una build di sviluppo |
| **Simulatore iOS** | Disponibile **solo su macOS** (richiede Xcode)                                                                  |
| **Cavo USB**       | Non necessario per Expo Go - basta il Wi-Fi                                                                     |

### 4.4 Usare il simulatore iOS (solo macOS)

1. Installa **Xcode** dall'App Store
2. Apri Xcode almeno una volta e accetta le licenze
3. Nel terminale Expo, premi **`i`** per aprire l'app nel simulatore iOS

---

## 5. Strumenti di debug

### 5.1 Console log (base)

I `console.log()` appaiono nel **terminale dove hai lanciato `npx expo start`**. Questo è il modo più veloce per verificare valori e flussi.

### 5.2 Developer Menu (sul telefono)

| Piattaforma           | Come aprirlo                                   |
| --------------------- | ---------------------------------------------- |
| **Android**           | Scuoti il telefono                             |
| **iPhone**            | Scuoti il telefono                             |
| **Emulatore Android** | `Ctrl + M` (Windows/Linux) o `Cmd + M` (macOS) |
| **Simulatore iOS**    | `Cmd + D`                                      |

Dal Developer Menu puoi:

- **Toggle Fast Refresh** - ricarica automatica quando salvi un file
- **Open JS Debugger** - apre il debugger nel browser
- **Show Performance Monitor** - mostra FPS e memoria

### 5.3 React DevTools (avanzato)

```bash
# Installa globalmente
npm install -g react-devtools

# Avvia in una finestra separata
react-devtools
```

Poi nel Developer Menu del telefono, React DevTools si collegherà automaticamente.

---

## 6. Troubleshooting

| Problema                     | Soluzione                                                                       |
| ---------------------------- | ------------------------------------------------------------------------------- |
| QR code non si collega       | Verifica che telefono e PC siano sulla **stessa rete Wi-Fi**                    |
| "Network response timed out" | Usa `npx expo start --tunnel`                                                   |
| Metro bundler bloccato       | Ferma con `Ctrl + C`, poi `npx expo start -c` (cancella cache)                  |
| `adb devices` lista vuota    | Controlla che il Debug USB sia attivo e accetta il prompt sul telefono          |
| App non si aggiorna          | Verifica che **Fast Refresh** sia attivo (Developer Menu)                       |
| "Expo Go is not compatible"  | Aggiorna Expo Go dallo store e aggiorna le dipendenze: `npx expo install --fix` |
| iPhone non apre il link      | Installa/aggiorna Expo Go dall'App Store                                        |

---

## 7. Comandi rapidi

```bash
# Avvia (default: LAN)
npx expo start

# Avvia con tunnel (Wi-Fi restrittivi)
npx expo start --tunnel

# Reset cache
npx expo start -c

# Apri su Android (emulatore o USB)
# Premi 'a' nel terminale

# Apri su iOS (solo macOS + Xcode)
# Premi 'i' nel terminale

# Verifica dispositivi Android collegati
adb devices

# Riavvia adb se non risponde
adb kill-server && adb start-server
```
