# Lab 14 – Soluzione

> **Deep linking (URL, errori, screenshot):** [Cheat Sheet §26](../labs/00_cheatsheet_react-native-programming_en.md#26--deep-linking).

## Cosa mostra la soluzione

- Stessa app del **Lab 13** (`FlatList` → Details con validazione `id` e item non trovato).
- Deep linking config con `prefixes` (`Linking.createURL("/")` per Expo Go + `myapp://` per dev build) e `config.screens`.
- `route.params.id` popolato sia da navigazione normale sia da URL (`details/:id`).
- Edge case: id mancante e item non trovato (stessi messaggi del Lab 13).

## Due terminali - emulatore + Metro + deep link

**Due terminali** in parallelo (vedi anche il lab 14):

| Terminale | Ruolo                                                                         |
| --------- | ----------------------------------------------------------------------------- |
| **1**     | Emulatore (`adb devices`). Test deep link con **Expo Go**: vedi comando sotto |
| **2**     | `cd MyFirstApp` → `npx expo start` → premi `a` - **non chiudere** Metro       |

### Test (Expo Go, emulatore Android)

**Terminale 2:** Metro avviato, app su schermata Home in Expo Go.

**Terminale 1:**

```bash
adb devices
npx uri-scheme open "exp://10.0.2.2:8081/--/details/a1" --android
```

Su telefono fisico: usa l'IP del PC dal terminale Metro, es. `exp://192.168.1.6:8081/--/details/a1`.

> **`myapp://` non funziona in Expo Go** - solo dopo `npx expo run:android`. Dettagli: [Cheat Sheet §26](../labs/00_cheatsheet_react-native-programming_en.md#26--deep-linking).

## Screenshot

**Lista items - FlatList con navigazione a dettaglio**

![Lab 13 - Lista items](../labs/imgs/lab_13_list.png)

**Dettaglio item - parametro id passato via route params**

![Lab 13 - Dettaglio item](../labs/imgs/lab_13_details_1.png)
![Lab 13 - Dettaglio item](../labs/imgs/lab_13_details_2.png)
![Lab 13 - Dettaglio item](../labs/imgs/lab_13_details_3.png)

## Codice

### app.json

```json
{
  "expo": {
    "scheme": "myapp",
    "name": "MyFirstApp",
    "slug": "MyFirstApp"
  }
}
```

### App.tsx

```tsx
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import * as Linking from "expo-linking";
import { HomeScreen } from "./src/screens/HomeScreen";
import { DetailsScreen } from "./src/screens/DetailsScreen";

const Stack = createNativeStackNavigator();

const linking = {
  prefixes: [Linking.createURL("/"), "myapp://"],
  config: {
    screens: {
      Home: "home",
      Details: "details/:id",
    },
  },
};

export default function App() {
  return (
    <NavigationContainer linking={linking}>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} options={{ title: "Items" }} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

### src/screens/HomeScreen.tsx

```tsx
import { FlatList, Pressable, StyleSheet, Text, View } from "react-native";

const DATA = [
  { id: "a1", title: "Alpha" },
  { id: "b2", title: "Beta" },
  { id: "c3", title: "Gamma" },
];

export function HomeScreen({ navigation }: any) {
  return (
    <View style={styles.container}>
      <FlatList
        data={DATA}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <Pressable
            style={styles.listItem}
            onPress={() => navigation.navigate("Details", { id: item.id })}
          >
            <Text>{item.title}</Text>
          </Pressable>
        )}
      />
      <Text style={styles.hint}>Expo Go test: exp://10.0.2.2:8081/--/details/a1</Text>
      <Text style={styles.hint}>Dev build: myapp://details/:id</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16 },
  listItem: {
    paddingVertical: 14,
    borderBottomWidth: 1,
    borderBottomColor: "#ccc",
  },
  hint: { marginTop: 12, color: "#666", fontSize: 13 },
});
```

### src/screens/DetailsScreen.tsx

```tsx
import { Pressable, StyleSheet, Text, View } from "react-native";

const DATA = [
  { id: "a1", title: "Alpha", description: "First item" },
  { id: "b2", title: "Beta", description: "Second item" },
  { id: "c3", title: "Gamma", description: "Third item" },
];

export function DetailsScreen({ navigation, route }: any) {
  const id = route.params?.id;
  if (!id) return <Text style={{ padding: 16 }}>Invalid route param</Text>;

  const item = DATA.find((x) => x.id === id);
  if (!item) return <Text style={{ padding: 16 }}>Product not found</Text>;

  return (
    <View style={styles.container}>
      <Text style={styles.title}>{item.title}</Text>
      <Text>{item.description}</Text>
      <Pressable style={styles.button} onPress={() => navigation.goBack()}>
        <Text style={styles.buttonText}>Go back</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, gap: 12 },
  title: { fontSize: 22, fontWeight: "700" },
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

## Test deep link - edge case

Link senza `id` (path incompleto):

```bash
npx uri-scheme open "exp://10.0.2.2:8081/--/details" --android
```

Atteso: schermata Details con messaggio **Invalid route param**.

Link con `id` inesistente:

```bash
npx uri-scheme open "exp://10.0.2.2:8081/--/details/xyz" --android
```

Atteso: schermata Details con messaggio **Product not found**.

## Test web (opzionale)

```bash
npx expo start --web
```

Nel browser:

```
http://localhost:8081/details/a1
```

Atteso: Details con Alpha. Su web: `http://` e path diretto `details/a1` - senza prefisso `/--/` (solo per `exp://` in Expo Go). Vedi [Cheat Sheet §26](../labs/00_cheatsheet_react-native-programming_en.md#26--deep-linking).
