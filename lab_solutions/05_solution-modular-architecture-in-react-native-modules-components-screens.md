# Lab 05 - Soluzione

## Cosa mostra la soluzione

- La mini app Notes del lab 04 spezzata in `App.tsx`, `screens/`, `components/`, `services/`.
- `PrimaryButton` estratto come componente riusabile.
- `UsersScreen` che mantiene la logica della schermata e richiama il service.
- `services/users.ts` che contiene i dati condivisi della feature.

## Due modi per separare il bottone

1. **Con `interface`**: definisci `PrimaryButtonProps` e destrutturi `label` e `onPress` nella funzione. Questa e la versione usata sotto.
2. **Con `props`**: ricevi `props: PrimaryButtonProps` e usi `props.label` / `props.onPress`. Questa variante e mostrata nei commenti del componente.

## File

```text
services/users.ts
components/PrimaryButton.tsx
screens/UsersScreen.tsx
App.tsx
```

## Codice

### services/users.ts

```ts
let notes: { id: string; text: string }[] = [];

function addMessage(text: string) {
  notes = [{ id: String(Date.now()), text }, ...notes];
}

export { addMessage, notes };
```

### components/PrimaryButton.tsx

```tsx
import { Pressable, StyleSheet, Text } from "react-native";

interface PrimaryButtonProps {
  label: string;
  onPress: () => void;
}

// // Alternative with props object:
// export function PrimaryButton(props: PrimaryButtonProps) {
//   return (
//     <Pressable onPress={props.onPress} style={styles.button}>
//       <Text style={styles.buttonText}>{props.label}</Text>
//     </Pressable>
//   );
// }

export function PrimaryButton({ label, onPress }: PrimaryButtonProps) {
  return (
    <Pressable onPress={onPress} style={styles.button}>
      <Text style={styles.buttonText}>{label}</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
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

### screens/UsersScreen.tsx

```tsx
import React from "react";
import { StyleSheet, Text, TextInput, View } from "react-native";
import { SafeAreaView } from "react-native-safe-area-context";
import { PrimaryButton } from "../components/PrimaryButton";
import { addMessage, notes } from "../services/users";

// type ScreenStatus = "loading" | "empty" | "success" | "error";

export default function UsersScreen() {
  const [text, setText] = React.useState("");
  // const [status, setStatus] = React.useState<ScreenStatus>("empty");
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
    addMessage(trimmed);
    setText("");
    load();
  }

  return (
    <SafeAreaView style={{ flex: 1 }}>
      <View style={styles.container}>
        <Text style={styles.title}>Notes</Text>
        <TextInput
          value={text}
          onChangeText={setText}
          placeholder="Write a note"
          style={styles.input}
        />

        <PrimaryButton label="Add" onPress={onAdd} />

        {status === "loading" && <Text>Caricamento...</Text>}
        {status === "empty" && <Text>Ancora niente qui</Text>}
        {status === "error" && <PrimaryButton label="Riprova" onPress={load} />}
        {status === "success" &&
          notes.map((note) => <Text key={note.id}>• {note.text}</Text>)}
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, gap: 12 },
  title: { fontSize: 20, fontWeight: "600" },
  input: { borderWidth: 1, padding: 12, borderRadius: 8 },
});
```

### App.tsx

```tsx
import { SafeAreaProvider } from "react-native-safe-area-context";
import UsersScreen from "./screens/UsersScreen";

export default function App() {
  return (
    <SafeAreaProvider>
      <UsersScreen />
    </SafeAreaProvider>
  );
}
```

## Screenshot

**Stesso stato empty del lab 04, ma con codice separato**

![Lab 05 - Stato empty](../labs/imgs/lab_04_empty.png)

**Una nota aggiunta dopo il refactor modulare**

![Lab 05 - Una nota aggiunta](../labs/imgs/lab_04_success_1.png)

**Struttura cartelle - components / screens / services**

![Lab 05 - Struttura cartelle](../labs/imgs/lab_05_structure.png)
