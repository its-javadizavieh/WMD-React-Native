# Lab 08 – Soluzione

## Cosa mostra la soluzione

- Componente riusabile `SettingRow` con props.
- `TextInput` e `Switch` collegati a `useState`.
- Edge case: nome troppo corto → messaggio di errore.

## Screenshot

![Lab 08 - Settings screen](../labs/imgs/lab_08_main.png)

![Lab 08 - Validazione nome](../labs/imgs/lab_08_validation.png)

## Codice

### components/SettingRow.tsx

```tsx
import React from "react";
import { Text, View } from "react-native";

export function SettingRow({
  label,
  value,
  right,
}: {
  label: string;
  value: string;
  right: React.ReactNode;
}) {
  return (
    <View
      style={{
        flexDirection: "row",
        alignItems: "center",
        paddingVertical: 12,
      }}
    >
      <View style={{ flex: 1 }}>
        <Text style={{ fontWeight: "600" }}>{label}</Text>
        <Text>{value}</Text>
      </View>
      <View>{right}</View>
    </View>
  );
}
```

### App.tsx

```tsx
import React from "react";
import { Switch, Text, TextInput, View } from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";
import { SettingRow } from "./components/SettingRow";

export default function App() {
  const [name, setName] = React.useState("");
  const [notify, setNotify] = React.useState(false);
  const nameOk = name.trim().length >= 2;

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <View style={{ flex: 1, padding: 16 }}>
          <SettingRow
            label="Name"
            value="Shown to other users"
            right={
              <TextInput
                value={name}
                onChangeText={setName}
                placeholder="Type name"
                style={{
                  borderWidth: 1,
                  borderRadius: 8,
                  padding: 8,
                  minWidth: 140,
                }}
              />
            }
          />
          {!nameOk && (
            <Text style={{ fontWeight: "700" }}>Name is too short</Text>
          )}
          <SettingRow
            label="Notifications"
            value="You can change later"
            right={<Switch value={notify} onValueChange={setNotify} />}
          />
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}
```
