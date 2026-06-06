# Lab 10 – Soluzione

## Cosa mostra la soluzione

- `useEffect` con timer e funzione di cleanup.
- Stati espliciti: loading → success / error.
- Edge case: cleanup cancella il timer.

## Screenshot

![Lab 10 - Stato loading](../labs/imgs/lab_10_loading.png)

![Lab 10 - Stato success](../labs/imgs/lab_10_success.png)

![Lab 10 - Stato error](../labs/imgs/lab_10_error.png)

## Codice

### App.tsx

```tsx
import React from "react";
import { Pressable, StyleSheet, Text, View } from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";

export default function App() {
  const [status, setStatus] = React.useState("loading");

  React.useEffect(() => {
    console.log("Screen mounted");
    const id = setTimeout(() => {
      setStatus("success");
    }, 1000);

    return () => clearTimeout(id);
  }, []);

  function onRetry() {
    setStatus("loading");
    setTimeout(() => setStatus("error"), 1000);
  }

  if (status === "loading") {
    return (
      <SafeAreaProvider>
        <SafeAreaView style={{ flex: 1 }}>
          <Text style={{ padding: 16 }}>Caricamento...</Text>
        </SafeAreaView>
      </SafeAreaProvider>
    );
  }
  if (status === "error") {
    return (
      <SafeAreaProvider>
        <SafeAreaView style={{ flex: 1 }}>
          <View style={styles.container}>
            <Text>Caricamento fallito</Text>
            <Pressable onPress={onRetry} style={styles.button}>
              <Text style={styles.buttonText}>Riprova</Text>
            </Pressable>
          </View>
        </SafeAreaView>
      </SafeAreaProvider>
    );
  }

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Todos</Text>
          <Text>Fatto ✓</Text>
          <Pressable onPress={onRetry} style={styles.button}>
            <Text style={styles.buttonText}>Reload</Text>
          </Pressable>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, gap: 12 },
  title: { fontSize: 20, fontWeight: "600" },
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
