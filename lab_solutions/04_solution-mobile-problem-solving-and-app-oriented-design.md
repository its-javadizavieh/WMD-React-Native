# Lab 04 – Soluzione

## Cosa mostra la soluzione

- Stati espliciti: loading / empty / success / error.
- Retry su errore con funzione `load()`.
- Edge case: stato error con azione retry.

## Codice

### App.tsx

```tsx
import React from "react";
import { Pressable, StyleSheet, Text, TextInput, View } from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";

let notes: { id: string; text: string }[] = [];

function addNote(text: string) {
  notes = [{ id: String(Date.now()), text }, ...notes];
}

export default function App() {
  const [text, setText] = React.useState("");
  const [status, setStatus] = React.useState("empty");
  const [, refresh] = React.useState(0);

  function load() {
    setStatus("loading");
    setTimeout(() => {
      setStatus(notes.length ? "success" : "empty");
      refresh((n) => n + 1);
    }, 300);
  }

  React.useEffect(() => {
    load();
  }, []);

  function onAdd() {
    const trimmed = text.trim();
    if (!trimmed) return;
    addNote(trimmed);
    setText("");
    load();
  }

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Notes</Text>
          <TextInput
            value={text}
            onChangeText={setText}
            placeholder="Write a note"
            style={styles.input}
          />
          <Pressable style={styles.button} onPress={onAdd}>
            <Text style={styles.buttonText}>Add</Text>
          </Pressable>
          {status === "loading" && <Text>Caricamento...</Text>}
          {status === "empty" && <Text>Ancora niente qui</Text>}
          {status === "error" && (
            <Pressable style={styles.button} onPress={load}>
              <Text style={styles.buttonText}>Riprova</Text>
            </Pressable>
          )}
          {status === "success" &&
            notes.map((n) => <Text key={n.id}>• {n.text}</Text>)}
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, gap: 12 },
  title: { fontSize: 20, fontWeight: "600" },
  input: { borderWidth: 1, padding: 12, borderRadius: 8 },
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

## Screenshot

**Stato empty — nessuna nota, messaggio fallback**

![Lab 04 – Stato empty](../labs/imgs/lab_04_empty.png)

**Una nota aggiunta**

![Lab 04 – Una nota aggiunta](../labs/imgs/lab_04_success_1.png)

**Due note aggiunte**

![Lab 04 – Due note aggiunte](../labs/imgs/lab_04_success_2.png)
