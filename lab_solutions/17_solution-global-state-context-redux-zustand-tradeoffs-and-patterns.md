# Lab 17 – Soluzione (Italian Meals App)

## Cosa mostra la soluzione

- **FavoritesContext** con load al mount e persist al toggle.
- **FavoritesScreen** filtra piatti italiani con `fetchItalianMeals()`.
- AsyncStorage solo in `services/storage.ts`.

## File

```text
services/mealsApi.ts
services/storage.ts
App.tsx
context/FavoritesContext.tsx
screens/MealsScreen.tsx
```

## Screenshot

**Lista piatti - preferiti attivi condivisi via Context**

![Lab 17 - Lista preferiti attivi](../labs/imgs/lab_17_favorites_list.png)

**Schermata Preferiti - stessi idMeal filtrati dalla lista**

![Lab 17 - Schermata preferiti](../labs/imgs/lab_17_favorites_screen.png)

## Codice

### services/mealsApi.ts

```ts
const BASE = "https://www.themealdb.com/api/json/v1/1";

export async function fetchItalianMeals() {
  const res = await fetch(`${BASE}/filter.php?a=Italian`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const data = await res.json();
  return data.meals ?? [];
}

export async function fetchMealById(id: string) {
  const res = await fetch(`${BASE}/lookup.php?i=${id}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const data = await res.json();
  return data.meals?.[0] ?? null;
}
```

### services/storage.ts

```ts
import AsyncStorage from "@react-native-async-storage/async-storage";

export const FAVORITES_KEY = "app:v1:favs";

export async function loadFavoriteIds(): Promise<string[]> {
  try {
    const raw = await AsyncStorage.getItem(FAVORITES_KEY);
    if (!raw) return [];
    const parsed = JSON.parse(raw) as unknown;
    return Array.isArray(parsed)
      ? parsed.filter((id): id is string => typeof id === "string")
      : [];
  } catch {
    return [];
  }
}

export async function saveFavoriteIds(ids: string[]): Promise<void> {
  try {
    await AsyncStorage.setItem(FAVORITES_KEY, JSON.stringify(ids));
  } catch {
    // ignora errori storage in dev
  }
}
```

### App.tsx (Provider tree)

```tsx
import { SafeAreaProvider } from "react-native-safe-area-context";
import { FavoritesProvider } from "./context/FavoritesContext";
import { MealsScreen } from "./screens/MealsScreen";

export default function App() {
  return (
    <SafeAreaProvider>
      <FavoritesProvider>
        <MealsScreen />
      </FavoritesProvider>
    </SafeAreaProvider>
  );
}
```

### context/FavoritesContext.tsx

```tsx
import React from "react";
import { loadFavoriteIds, saveFavoriteIds } from "../services/storage";

interface FavoritesContextValue {
  favoriteIds: string[];
  isLoading: boolean;
  isFavorite: (idMeal: string) => boolean;
  toggleFavorite: (idMeal: string) => void;
}

const FavoritesContext = React.createContext<FavoritesContextValue | null>(null);

export function FavoritesProvider({ children }: { children: React.ReactNode }) {
  const [favoriteIds, setFavoriteIds] = React.useState<string[]>([]);
  const [isLoading, setIsLoading] = React.useState(true);

  React.useEffect(() => {
    loadFavoriteIds()
      .then(setFavoriteIds)
      .catch(() => setFavoriteIds([]))
      .finally(() => setIsLoading(false));
  }, []);

  function persist(ids: string[]) {
    setFavoriteIds(ids);
    void saveFavoriteIds(ids);
  }

  function isFavorite(idMeal: string) {
    return favoriteIds.includes(idMeal);
  }

  function toggleFavorite(idMeal: string) {
    persist(
      favoriteIds.includes(idMeal)
        ? favoriteIds.filter((id) => id !== idMeal)
        : [...favoriteIds, idMeal],
    );
  }

  const value = React.useMemo(
    () => ({ favoriteIds, isLoading, isFavorite, toggleFavorite }),
    [favoriteIds, isLoading],
  );

  return (
    <FavoritesContext.Provider value={value}>{children}</FavoritesContext.Provider>
  );
}

export function useFavorites() {
  const context = React.useContext(FavoritesContext);
  if (!context) {
    throw new Error("useFavorites must be used within FavoritesProvider");
  }
  return context;
}
```

### context/FavoritesContext.tsx

```tsx
import React from "react";
import {
  ActivityIndicator,
  FlatList,
  Image,
  Pressable,
  StyleSheet,
  Text,
  View,
} from "react-native";
import { SafeAreaView } from "react-native-safe-area-context";
import { useFavorites } from "../context/FavoritesContext";
import { fetchItalianMeals } from "../services/mealsApi";

interface MealSummary {
  idMeal: string;
  strMeal: string;
  strMealThumb: string;
}

export function MealsScreen() {
  const { favoriteIds, isLoading: favoritesLoading, isFavorite, toggleFavorite } =
    useFavorites();
  const [view, setView] = React.useState<"meals" | "favorites">("meals");
  const [state, setState] = React.useState<{
    status: "idle" | "loading" | "success" | "error";
    items: MealSummary[];
    message: string;
  }>({
    status: "idle",
    items: [],
    message: "",
  });

  async function loadMeals() {
    setState({ status: "loading", items: [], message: "" });
    try {
      const data = await fetchItalianMeals();
      setState({ status: "success", items: data, message: "" });
    } catch {
      setState({
        status: "error",
        items: [],
        message: "Impossibile caricare i piatti.",
      });
    }
  }

  React.useEffect(() => {
    loadMeals();
  }, []);

  const visibleMeals =
    view === "favorites"
      ? state.items.filter((meal) => favoriteIds.includes(meal.idMeal))
      : state.items;

  if (favoritesLoading || state.status === "loading") {
    return (
      <SafeAreaView style={styles.centered}>
        <ActivityIndicator />
        <Text>Caricamento...</Text>
      </SafeAreaView>
    );
  }

  if (state.status === "error") {
    return (
      <SafeAreaView style={styles.container}>
        <Text style={styles.error}>{state.message}</Text>
        <Pressable style={styles.button} onPress={loadMeals}>
          <Text style={styles.buttonText}>Retry</Text>
        </Pressable>
      </SafeAreaView>
    );
  }

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>
        {view === "meals" ? "Piatti italiani" : "I tuoi preferiti"}
      </Text>
      <View style={styles.tabs}>
        <Pressable style={styles.tab} onPress={() => setView("meals")}>
          <Text style={styles.tabText}>Lista</Text>
        </Pressable>
        <Pressable style={styles.tab} onPress={() => setView("favorites")}>
          <Text style={styles.tabText}>Preferiti ({favoriteIds.length})</Text>
        </Pressable>
      </View>

      {view === "favorites" && visibleMeals.length === 0 ? (
        <Text>Nessun preferito ancora. Tocca ♡ su un piatto dalla lista.</Text>
      ) : (
        <FlatList
          data={visibleMeals}
          keyExtractor={(item) => item.idMeal}
          renderItem={({ item }) => (
            <View style={styles.row}>
              <Image source={{ uri: item.strMealThumb }} style={styles.thumb} />
              <Text style={styles.mealName} numberOfLines={2}>
                {item.strMeal}
              </Text>
              <Pressable
                style={styles.favButton}
                onPress={() => toggleFavorite(item.idMeal)}
              >
                <Text style={styles.favText}>
                  {isFavorite(item.idMeal) ? "♥" : "♡"}
                </Text>
              </Pressable>
            </View>
          )}
        />
      )}
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, gap: 12 },
  centered: { flex: 1, padding: 16, gap: 8, justifyContent: "center" },
  title: { fontSize: 22, fontWeight: "700" },
  tabs: { flexDirection: "row", gap: 8 },
  tab: { paddingVertical: 8, paddingHorizontal: 12, borderWidth: 1, borderRadius: 8 },
  tabText: { fontWeight: "600" },
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
  row: {
    flexDirection: "row",
    alignItems: "center",
    gap: 12,
    paddingVertical: 12,
    borderBottomWidth: 1,
    borderBottomColor: "#ccc",
  },
  thumb: { width: 48, height: 48, borderRadius: 8 },
  mealName: { flex: 1, fontWeight: "600" },
  favButton: { padding: 8, borderWidth: 1, borderRadius: 8 },
  favText: { fontSize: 18 },
});
```

> Nel **progetto finale** aggiungi anche `ThemeProvider` (lab 19) nello stesso albero.
