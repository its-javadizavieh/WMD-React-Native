# Lab 06 – Soluzione

## Cosa mostra la soluzione

- `fetch` con controllo `res.ok` per errori HTTP.
- Visualizzazione lista con `FlatList`.
- Edge case: errore HTTP gestito con retry.

## Codice

### App.tsx

```tsx
import React from "react";
import { FlatList, Pressable, StyleSheet, Text, View } from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";

async function fetchTodos() {
  const res = await fetch(
    "https://jsonplaceholder.typicode.com/todos?_limit=5",
  );
  if (!res.ok) throw new Error("Request failed");
  return res.json();
}

interface FlatListProps {
  id: number;
  title: string;
  completed: boolean;
}

export default function App() {
  // const [todos, setTodos] = React.useState<FlatListProps[]>([]);
  const [todos, setTodos] = React.useState([]);
  const [status, setStatus] = React.useState("loading");

  function load() {
    setStatus("loading");
    fetchTodos()
      .then((data) => {
        setTodos(data);
        setStatus("success");
      })
      .catch(() => setStatus("error"));
  }

  React.useEffect(() => {
    load();
  }, []);

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Todos</Text>
          {status === "loading" && <Text>Loading…</Text>}
          {status === "error" && (
            <Pressable onPress={load} style={styles.button}>
              <Text style={styles.buttonText}>Retry</Text>
            </Pressable>
          )}
          {status === "success" && (
            <FlatList<FlatListProps>
              data={todos}
              keyExtractor={(item) => String(item.id)}
              renderItem={({ item }) => (
                <Text style={{ paddingVertical: 8 }}>
                  {item.completed ? "✓" : "○"} {item.title}
                </Text>
              )}
            />
          )}
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

## Screenshot

**Stato loading - caricamento todos**

![Lab 06 – Stato loading](../labs/imgs/lab_06_main_1.png)

**Todos caricati da API**

![Lab 06 – Todos caricati](../labs/imgs/lab_06_main_2.png)

**Stato errore - pulsante Retry**

![Lab 06 – Stato errore](../labs/imgs/lab_06_error.png)
