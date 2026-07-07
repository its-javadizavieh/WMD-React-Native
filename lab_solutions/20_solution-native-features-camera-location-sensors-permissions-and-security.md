# Lab 20 – Soluzione (Italian Meals App)

## Cosa mostra la soluzione

- Sezione **«La tua posizione»** integrata in `SettingsScreen`.
- Bootstrap al mount con `getForegroundPermissionsAsync()`.
- UI per stati unknown / denied / granted / loading / error.
- Edge case: permesso negato → Settings; GPS non disponibile → fallback.

## Screenshot

![Lab 20 - Permesso richiesto](../labs/imgs/lab_20_permission.png)

![Lab 20 - Location ottenuta](../labs/imgs/lab_20_location.png)

## File

```text
App.tsx
```

## Codice

### App.tsx

```tsx
import React from "react";
import { Linking, Pressable, StyleSheet, Text, View } from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";
import * as Location from "expo-location";

type PermissionState = "unknown" | "denied" | "granted";
type LocationState = "idle" | "loading" | "ready" | "error";

function formatCoords(pos: Location.LocationObject) {
  return `Lat: ${pos.coords.latitude.toFixed(5)} | Lng: ${pos.coords.longitude.toFixed(5)}`;
}

async function readPosition(): Promise<Location.LocationObject> {
  try {
    return await Location.getCurrentPositionAsync({
      accuracy: Location.Accuracy.Balanced,
    });
  } catch {
    const last = await Location.getLastKnownPositionAsync();
    if (last) return last;
    throw new Error(
      "GPS non disponibile. Attiva la posizione e riprova.",
    );
  }
}

export default function App() {
  const [bootstrapping, setBootstrapping] = React.useState(true);
  const [permission, setPermission] =
    React.useState<PermissionState>("unknown");
  const [locationState, setLocationState] =
    React.useState<LocationState>("idle");
  const [coords, setCoords] = React.useState("");
  const [error, setError] = React.useState("");

  React.useEffect(() => {
    Location.getForegroundPermissionsAsync()
      .then(({ status }) => {
        if (status === "granted") setPermission("granted");
        else if (status === "denied") setPermission("denied");
        else setPermission("unknown");
      })
      .finally(() => setBootstrapping(false));
  }, []);

  async function onReadLocation() {
    setError("");
    const { status } = await Location.requestForegroundPermissionsAsync();
    if (status !== "granted") {
      setPermission("denied");
      setLocationState("idle");
      return;
    }

    setPermission("granted");
    setLocationState("loading");

    try {
      const pos = await readPosition();
      setCoords(formatCoords(pos));
      setLocationState("ready");
    } catch (err) {
      setLocationState("error");
      setError(
        err instanceof Error
          ? err.message
          : "GPS non disponibile. Attiva la posizione e riprova.",
      );
    }
  }

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Italian Meals</Text>
          <Text style={styles.subtitle}>Impostazioni · La tua posizione</Text>

          {bootstrapping && <Text>Controllo permesso…</Text>}

          {!bootstrapping && permission === "unknown" && (
            <Text>Tocca il pulsante per consentire l&apos;accesso alla posizione.</Text>
          )}

          {!bootstrapping && permission === "denied" && (
            <View style={{ gap: 12 }}>
              <Text>Permesso posizione negato.</Text>
              <Pressable
                style={styles.button}
                onPress={() => Linking.openSettings()}
              >
                <Text style={styles.buttonText}>Apri Impostazioni</Text>
              </Pressable>
            </View>
          )}

          {!bootstrapping &&
            permission === "granted" &&
            locationState === "idle" && (
              <Text>Permesso concesso. Tocca il pulsante per leggere le coordinate.</Text>
            )}

          {!bootstrapping &&
            permission === "granted" &&
            locationState === "loading" && <Text>Lettura coordinate…</Text>}

          {!bootstrapping &&
            permission === "granted" &&
            locationState === "ready" && <Text>{coords}</Text>}

          {!bootstrapping &&
            permission === "granted" &&
            locationState === "error" && <Text style={styles.error}>{error}</Text>}

          <Pressable style={styles.button} onPress={onReadLocation}>
            <Text style={styles.buttonText}>Leggi posizione</Text>
          </Pressable>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, gap: 12 },
  title: { fontSize: 22, fontWeight: "700" },
  subtitle: { color: "#555" },
  error: { color: "#B00020" },
  button: {
    alignSelf: "flex-start",
    paddingVertical: 10,
    paddingHorizontal: 16,
    borderWidth: 1,
    borderRadius: 8,
    backgroundColor: "#f0f0f0",
  },
  buttonText: { fontWeight: "600" },
});
```
