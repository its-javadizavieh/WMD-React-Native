# Lab 21 – Soluzione (Italian Meals App)

## Cosa mostra la soluzione

- Sezione **«Promemoria»** integrata in `SettingsScreen` (o componente dedicato).
- Import statico da `expo-notifications/build/...` (solo API locali).
- Canale Android + scheduling a 5 secondi — titolo **Promemoria**, body **Apri l'app!**
- UI in italiano per ogni stato permesso.
- Edge case: permesso negato → **Apri Impostazioni**.

## Screenshot

**Schermata Impostazioni - sezione notifiche**

![Lab 21 - Schermata iniziale](../labs/imgs/lab_21_main.png)
![Lab 21 - Schermata iniziale](../labs/imgs/lab_21_main_1.png)
![Lab 21 - Schermata iniziale](../labs/imgs/lab_21_deny.png)

**Notifica schedulata**

![Lab 21 - Notifica schedulata](../labs/imgs/lab_21_scheduled.png)

**Notifica pubblicata**

![Lab 21 - Notifica pubblicata](../labs/imgs/lab_21_published.png)

## File

```text
App.tsx
```

## Codice

### App.tsx (root)

```tsx
import React from "react";
import {
  Linking,
  Platform,
  Pressable,
  StyleSheet,
  Text,
  View,
} from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";
import { setNotificationHandler } from "expo-notifications/build/NotificationsHandler";
import {
  getPermissionsAsync,
  requestPermissionsAsync,
} from "expo-notifications/build/NotificationPermissions";
import { scheduleNotificationAsync } from "expo-notifications/build/scheduleNotificationAsync";
import { setNotificationChannelAsync } from "expo-notifications/build/setNotificationChannelAsync";
import { SchedulableTriggerInputTypes } from "expo-notifications/build/Notifications.types";
import { AndroidImportance } from "expo-notifications/build/NotificationChannelManager.types";

setNotificationHandler({
  handleNotification: async () => ({
    shouldPlaySound: false,
    shouldSetBadge: false,
    shouldShowBanner: true,
    shouldShowList: true,
  }),
});

type PermissionState = "unknown" | "denied" | "granted";
type ScheduleState = "idle" | "scheduled" | "error";

async function ensureAndroidChannel() {
  if (Platform.OS !== "android") return;
  try {
    await setNotificationChannelAsync("default", {
      name: "Promemoria",
      importance: AndroidImportance.DEFAULT,
    });
  } catch {
    // In Expo Go il provider dei canali può non essere disponibile:
    // la notifica locale funziona comunque, quindi ignoriamo l'errore.
  }
}

export default function App() {
  const [bootstrapping, setBootstrapping] = React.useState(true);
  const [permission, setPermission] =
    React.useState<PermissionState>("unknown");
  const [scheduleState, setScheduleState] =
    React.useState<ScheduleState>("idle");
  const [message, setMessage] = React.useState("");

  React.useEffect(() => {
    ensureAndroidChannel()
      .then(() => getPermissionsAsync())
      .then(({ status }) => {
        if (status === "granted") setPermission("granted");
        else if (status === "denied") setPermission("denied");
        else setPermission("unknown");
      })
      .catch(() => setPermission("unknown"))
      .finally(() => setBootstrapping(false));
  }, []);

  async function onSchedule() {
    setScheduleState("idle");
    setMessage("");

    try {
      await ensureAndroidChannel();

      const { status } = await requestPermissionsAsync({
        ios: { allowAlert: true, allowBadge: true, allowSound: true },
      });

      if (status !== "granted") {
        setPermission("denied");
        return;
      }

      setPermission("granted");

      await scheduleNotificationAsync({
        content: { title: "Promemoria", body: "Apri l'app!" },
        trigger: {
          type: SchedulableTriggerInputTypes.TIME_INTERVAL,
          seconds: 5,
        },
      });
      setScheduleState("scheduled");
    } catch (err) {
      setScheduleState("error");
      setMessage(
        err instanceof Error
          ? err.message
          : "Impossibile schedulare la notifica.",
      );
    }
  }

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Italian Meals</Text>
          <Text style={styles.subtitle}>Impostazioni · Promemoria</Text>

          {bootstrapping && <Text>Controllo permesso…</Text>}

          {!bootstrapping && permission === "unknown" && (
            <Text>
              Tocca il pulsante: l&apos;app chiederà il permesso per le
              notifiche, poi schedulerà un promemoria tra 5 secondi.
            </Text>
          )}

          {!bootstrapping && permission === "denied" && (
            <View style={{ gap: 12 }}>
              <Text>Permesso notifiche negato.</Text>
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
            scheduleState === "idle" && (
              <Text>Permesso concesso. Tocca il pulsante per schedulare.</Text>
            )}

          {!bootstrapping && scheduleState === "scheduled" && (
            <Text>Notifica schedulata. Attendi ~5 secondi.</Text>
          )}

          {!bootstrapping && scheduleState === "error" && (
            <Text style={styles.error}>{message}</Text>
          )}

          <Pressable style={styles.button} onPress={onSchedule}>
            <Text style={styles.buttonText}>Schedula promemoria tra 5s</Text>
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

> **Background tasks:** documenta nel README che il sistema operativo può ritardare o bloccare notifiche in background (risparmio batteria, Doze su Android). Per il corso basta la notifica locale schedulata in foreground.
