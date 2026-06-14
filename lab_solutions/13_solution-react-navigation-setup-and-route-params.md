# Lab 13 – Soluzione

## Cosa mostra la soluzione

- Setup `NavigationContainer` + stack navigator.
- Lista con `FlatList` → navigazione a dettaglio.
- Validazione `id` + item non trovato.
- Edge case: id mancante e item non trovato.

> **Lab 14:** riusa questo codice e aggiungi solo deep linking in `App.tsx` (vedi soluzione Lab 14).

## Screenshot

![Lab 13 - Lista items](../labs/imgs/lab_13_list.png)

![Lab 13 - Dettaglio item](../labs/imgs/lab_13_details.png)

## Codice

### App.tsx

```tsx
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import { HomeScreen } from "./src/screens/HomeScreen";
import { DetailsScreen } from "./src/screens/DetailsScreen";

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
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
