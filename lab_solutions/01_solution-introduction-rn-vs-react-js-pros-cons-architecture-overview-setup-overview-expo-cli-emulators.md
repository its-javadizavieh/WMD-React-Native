# Lab 01 – Soluzione

## Cosa mostra la soluzione

- Setup Expo + Metro + Fast Refresh funzionanti.
- Componente con prop `name` e interazione base.
- Edge case: nome vuoto → fallback "student".

## Codice

### App.tsx

```tsx
import React from "react";
import { Pressable, StyleSheet, Text, View } from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";

function Greeting({ name }: { name: string }) {
  return <Text>Hello {name || "student"}</Text>;
}

export default function App() {
  const [count, setCount] = React.useState(0);

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={styles.container}>
          <Text style={styles.title}>Hello React Native</Text>
          <Greeting name="Ada" />
          <Text>Count: {count}</Text>
          <Pressable style={styles.button} onPress={() => setCount((c) => c + 1)}>
            <Text style={styles.buttonText}>Increment</Text>
          </Pressable>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, justifyContent: "center", gap: 12 },
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
