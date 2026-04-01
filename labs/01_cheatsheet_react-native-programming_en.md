---
marp: true
theme: course-templates
paginate: true
size: 16:9
---

<!-- _class: cover -->
| DOCENTE | Seyedhossein Javadizavieh |
| UNITA' FORMATIVA | React Native |
| ARGOMENTO | React Native Programming - Cheat Sheet |

---

## 1 · Project setup (Expo)

```tsx
// Create a new project
npx create-expo-app MyApp
cd MyApp

// Start the dev server
npx expo start

// Run on a specific platform
npx expo start --android
npx expo start --ios
```

- **Fast Refresh** - save a file and changes appear instantly
- Press `r` in terminal to **reload**, `m` to open **dev menu**
- Use `npx expo install <pkg>` to install **compatible** versions

---

## 2 · Core component imports

```tsx
import {
  View,          // container (like <div>)
  Text,          // all text must be inside <Text>
  Image,         // local or remote images
  TextInput,     // text field
  Pressable,     // tappable wrapper (replaces TouchableOpacity)
  ScrollView,    // scrollable area (small content)
  FlatList,      // virtualized list (large content)
  SectionList,   // grouped virtualized list
  ActivityIndicator, // spinner
  Switch,        // toggle
  Modal,         // overlay dialog
  StatusBar,     // control status bar appearance
  StyleSheet,    // create optimized style objects
} from 'react-native';
```

---

## 3 · View - the universal container

```tsx
// View is a flexbox container (column by default)
<View style={{ flex: 1, padding: 16, gap: 12 }}>
  <Text>First</Text>
  <Text>Second</Text>
</View>
```

- Every layout starts with **View**
- Defaults to `flexDirection: 'column'`
- Use `gap` for spacing between children (RN 0.71+)
- **Cannot** display raw text - always wrap in `<Text>`

---

## 4 · Text - rendering text content

```tsx
// Basic text with inline styles
<Text style={{ fontSize: 18, fontWeight: '600', color: '#333' }}>
  Hello React Native
</Text>

// Nested text inherits parent styles
<Text style={{ fontSize: 16 }}>
  Normal <Text style={{ fontWeight: 'bold' }}>Bold</Text> normal
</Text>

// Truncation
<Text numberOfLines={2} ellipsizeMode="tail">
  Very long text that will be cut after two lines...
</Text>
```

---

## 5 · Image - local and remote

```tsx
// Remote image (must set width + height)
<Image
  source={{ uri: 'https://example.com/photo.jpg' }}
  style={{ width: 200, height: 150, borderRadius: 12 }}
/>

// Local image (dimensions auto-detected)
<Image
  source={require('./assets/logo.png')}
  style={{ width: 100, height: 100 }}
  resizeMode="contain"
/>
```

**resizeMode** values: `cover` | `contain` | `stretch` | `center`

---

## 6 · Pressable - handling taps

```tsx
// Pressable with visual feedback
<Pressable
  onPress={() => console.log('Tapped!')}
  onLongPress={() => console.log('Long press!')}
  style={({ pressed }) => ({
    opacity: pressed ? 0.6 : 1,
    padding: 14,
    backgroundColor: '#007AFF',
    borderRadius: 8,
  })}
>
  <Text style={{ color: '#fff', textAlign: 'center' }}>
    Tap me
  </Text>
</Pressable>
```

- Prefer **Pressable** over `TouchableOpacity` (newer API)
- `style` accepts a **function** for pressed state feedback

---

## 7 · ScrollView vs FlatList

```tsx
interface Item {
  id: string;
  title: string;
}

// ScrollView - renders ALL children at once
<ScrollView contentContainerStyle={{ padding: 16 }}>
  <Text>Item 1</Text>
  <Text>Item 2</Text>
</ScrollView>

// FlatList - virtualised, only renders visible rows
<FlatList<Item>
  data={items}
  keyExtractor={(item: Item) => item.id}
  renderItem={({ item }: { item: Item }) => <Text>{item.name}</Text>}
  ListEmptyComponent={<Text>No items</Text>}
/>
```

| Use case | Component |
|---|---|
| < 50 items, mixed content | **ScrollView** |
| Large list, uniform rows | **FlatList** |
| Grouped sections | **SectionList** |

---

## 8 · TextInput - controlled input

```tsx
const [email, setEmail] = React.useState('');

// Controlled: value always reflects state
<TextInput
  value={email}
  onChangeText={setEmail}
  placeholder="Email"
  keyboardType="email-address"
  autoCapitalize="none"
  autoCorrect={false}
  style={{
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 8,
    padding: 12,
    color: '#fff',
  }}
/>
```

Common **keyboardType** values: `default` | `email-address` | `numeric` | `phone-pad`

---

## 9 · useState - reactive state

```tsx
import React from 'react';

// Declare state with initial value
const [count, setCount] = React.useState(0);
const [items, setItems] = React.useState<string[]>([]);
const [user, setUser] = React.useState<{ name: string } | null>(null);

// Update state (triggers re-render)
setCount(10);
setCount((prev) => prev + 1);

// Update object/array state (immutable patterns)
setUser((prev) => ({ ...prev, name: 'Ada' }));
setItems((prev) => [...prev, newItem]);
setItems((prev) => prev.filter((i) => i.id !== id));
```

- State is **immutable** - always create a new reference
- Use **callback form** when new value depends on previous

---

## 10 · useEffect - side effects and cleanup

```tsx
// Run once on mount
React.useEffect(() => {
  fetchData();
}, []);

// Run when dependency changes
React.useEffect(() => {
  filterResults(query);
}, [query]);

// Cleanup on unmount (subscriptions, timers)
React.useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id);
}, []);
```

| Dependency array | Runs when |
|---|---|
| `[]` | Once on **mount** |
| `[a, b]` | When **a** or **b** changes |
| *(omitted)* | Every render (avoid) |

---

## 11a · StyleSheet

```tsx
const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
    gap: 12,
  },
  card: {
    padding: 16,
    backgroundColor: '#1e1e1e',
    borderRadius: 12,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.25,
    shadowRadius: 4,
    elevation: 5,
  },
});
```

- `StyleSheet.create` validates and **optimises** style objects
- Combine styles: `style={[styles.card, { marginTop: 8 }]}`

---

## 11b · Flexbox quick reference

| Property | Values |
|---|---|
| **flexDirection** | `column` (default), `row` |
| **justifyContent** | `flex-start`, `center`, `flex-end` |
| | `space-between`, `space-around`, `space-evenly` |
| **alignItems** | `stretch` (default), `flex-start`, `center`, `flex-end` |
| **flexWrap** | `nowrap` (default), `wrap` |
| **gap** | number (e.g. `12`) - spacing between children |
| **flex** | `1` - fill available space |
| **alignSelf** | override parent `alignItems` for one child |
| **position** | `relative` (default), `absolute` |

---

## 12 · Conditional rendering patterns

```tsx
interface Item {
  id: string;
  title: string;
}

// Short-circuit
{isLoading && <ActivityIndicator />}

// Ternary
{error ? <Text>{error}</Text> : <DataView data={data} />}

// Early return
if (loading) return <ActivityIndicator />;
if (error) return <Text>Error: {error}</Text>;
return <DataView data={data} />;

// Rendering a list
{items.map((item: Item) => (
  <Text key={item.id}>{item.name}</Text>
))}
```

---

## 13 · Forms - validation pattern

```tsx
const [email, setEmail] = React.useState('');
const [touched, setTouched] = React.useState(false);

const emailOk = email.includes('@');
const showError = touched && !emailOk;

<TextInput
  value={email}
  onChangeText={setEmail}
  onBlur={() => setTouched(true)}
  placeholder="Email"
/>

// Show error only after the user interacts
{showError && (
  <Text style={{ color: '#ff4444' }}>Invalid email</Text>
)}

// Disable submit until valid
<Pressable
  disabled={!emailOk}
  style={{ opacity: emailOk ? 1 : 0.4 }}
  onPress={handleSubmit}
>
  <Text>Submit</Text>
</Pressable>
```

---

## 14 · fetch - REST API calls

```tsx
// GET request
const response = await fetch('https://api.example.com/items');
const data = await response.json();

// POST request
const response = await fetch('https://api.example.com/items', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title: 'New item' }),
});

// DELETE request
await fetch(`https://api.example.com/items/${id}`, {
  method: 'DELETE',
});
```

---

## 15 · Async data pattern (load → show → error)

```tsx
interface Item {
  id: string;
  title: string;
}

const [data, setData] = React.useState<Item[] | null>(null);
const [loading, setLoading] = React.useState(true);
const [error, setError] = React.useState<string | null>(null);

React.useEffect(() => {
  const load = async () => {
    try {
      const res = await fetch(URL);
      const json = await res.json();
      setData(json);
    } catch (e) {
      setError(e.message);
    } finally {
      setLoading(false);
    }
  };
  load();
}, []);

// Render based on state
if (loading) return <ActivityIndicator />;
if (error) return <Text>Error: {error}</Text>;
return <FlatList<Item> data={data} /* ... */ />;
```

---

## 16 · React Navigation - setup

```tsx
// Install
npx expo install @react-navigation/native
npx expo install @react-navigation/native-stack
npx expo install react-native-screens react-native-safe-area-context

// App.tsx
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';


type RootStackParamList = {
  Home: undefined;
  Detail: { id: number };
};


const Stack = createNativeStackNavigator<RootStackParamList>();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Detail" component={DetailScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

---

## 17 · Navigation - navigate, params, goBack

```tsx
import type { NativeStackScreenProps } from '@react-navigation/native-stack';


type RootStackParamList = {
  [screen: string]: object | undefined;
};


// Navigate to a screen with params
function HomeScreen({ navigation }: NativeStackScreenProps<RootStackParamList>) {
  return (
    <Pressable
      onPress={() => navigation.navigate('Detail', { id: 42 })}
    >
      <Text>Go to Detail</Text>
    </Pressable>
  );
}

// Read params on the target screen
function DetailScreen({ route, navigation }: NativeStackScreenProps<RootStackParamList>) {
  const { id } = route.params;
  return (
    <View>
      <Text>Item ID: {id}</Text>
      <Pressable onPress={() => navigation.goBack()}>
        <Text>Back</Text>
      </Pressable>
    </View>
  );
}
```

---

## 18 · Tab and Drawer navigators

```tsx
// Bottom tabs
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
const Tab = createBottomTabNavigator();

<Tab.Navigator>
  <Tab.Screen name="Feed" component={FeedScreen} />
  <Tab.Screen name="Profile" component={ProfileScreen} />
</Tab.Navigator>

// Drawer
import { createDrawerNavigator } from '@react-navigation/drawer';
const Drawer = createDrawerNavigator();

<Drawer.Navigator>
  <Drawer.Screen name="Home" component={HomeScreen} />
  <Drawer.Screen name="Settings" component={SettingsScreen} />
</Drawer.Navigator>
```

- **Nest** navigators: Tab inside Stack, Drawer wrapping Stack

---

## 19 · AsyncStorage - local persistence

```tsx
import AsyncStorage from '@react-native-async-storage/async-storage';

// Save a value
await AsyncStorage.setItem('token', 'abc123');

// Save an object (must stringify)
await AsyncStorage.setItem('user', JSON.stringify(user));

// Read a value
const token = await AsyncStorage.getItem('token');

// Read an object (must parse)
const raw = await AsyncStorage.getItem('user');
const user = raw ? JSON.parse(raw) : null;

// Remove
await AsyncStorage.removeItem('token');

// Clear everything
await AsyncStorage.clear();
```

---

## 20 · Context - sharing state globally

```tsx
// 1. Create context
interface AuthValue {
  user: { name: string } | null;
  setUser: React.Dispatch<React.SetStateAction<{ name: string } | null>>;
}

const AuthContext = React.createContext<AuthValue | null>(null);

// 2. Provider wraps app tree
interface AuthProviderProps {
  children: React.ReactNode;
}

function AuthProvider({ children }: AuthProviderProps) {
  const [user, setUser] = React.useState<{ name: string } | null>(null);
  return (
    <AuthContext.Provider value={{ user, setUser }}>
      {children}
    </AuthContext.Provider>
  );
}

// 3. Consume anywhere with useContext
function ProfileScreen() {
  const { user } = React.useContext(AuthContext);
  return <Text>{user?.name ?? 'Guest'}</Text>;
}
```

- Context is for **low-frequency** updates (auth, theme, locale)
- For **high-frequency** state, prefer **Zustand** or **Redux**

---

## 21 · Zustand - lightweight global store

```tsx
import { create } from 'zustand';

// Define store
interface CartItem {
  id: string;
  name: string;
}

interface CartState {
  items: CartItem[];
  addItem: (item: CartItem) => void;
  removeItem: (id: string) => void;
  clear: () => void;
}

const useCartStore = create<CartState>((set) => ({
  items: [],
  addItem: (item) =>
    set((s) => ({ items: [...s.items, item] })),
  removeItem: (id) =>
    set((s) => ({ items: s.items.filter((i) => i.id !== id) })),
  clear: () => set({ items: [] }),
}));

// Use in any component (no Provider needed)
function CartBadge() {
  const count = useCartStore((s) => s.items.length);
  return <Text>Cart: {count}</Text>;
}
```

---

## 22 · Custom hooks - reusable logic

```tsx
// useFetch - generic data fetcher
function useFetch<T = unknown>(url: string) {
  const [data, setData] = React.useState<T | null>(null);
  const [loading, setLoading] = React.useState(true);
  const [error, setError] = React.useState<string | null>(null);

  React.useEffect(() => {
    let cancelled = false;
    (async () => {
      try {
        const res = await fetch(url);
        const json = await res.json();
        if (!cancelled) setData(json);
      } catch (e) {
        if (!cancelled) setError(e.message);
      } finally {
        if (!cancelled) setLoading(false);
      }
    })();
    return () => { cancelled = true; };
  }, [url]);

  return { data, loading, error };
}
```

---

## 23 · Responsive StyleSheet and Flexbox

```tsx
import { Dimensions, useWindowDimensions } from 'react-native';

// Hook (updates on rotation)
function MyComponent() {
  const { width, height } = useWindowDimensions();
  const isLandscape = width > height;

  return (
    <View style={{
      flexDirection: isLandscape ? 'row' : 'column',
      padding: width > 600 ? 32 : 16,
    }}>
      <Text>Adaptive layout</Text>
    </View>
  );
}

// Percentage-based
<View style={{ width: '80%', alignSelf: 'center' }} />
```

---

## 24 · Permissions (expo)

```tsx
import * as Location from 'expo-location';
import * as ImagePicker from 'expo-image-picker';

// Location
const { status } = await Location.requestForegroundPermissionsAsync();
if (status === 'granted') {
  const loc = await Location.getCurrentPositionAsync({});
  console.log(loc.coords.latitude, loc.coords.longitude);
}

// Camera / Gallery
const { status } = await ImagePicker.requestCameraPermissionsAsync();
if (status === 'granted') {
  const result = await ImagePicker.launchCameraAsync({
    allowsEditing: true,
    quality: 0.8,
  });
  if (!result.canceled) console.log(result.assets[0].uri);
}
```

---

## 25 · Notifications (expo)

```tsx
import * as Notifications from 'expo-notifications';

// Request permission
const { status } = await Notifications.requestPermissionsAsync();

// Schedule a local notification
await Notifications.scheduleNotificationAsync({
  content: {
    title: 'Reminder',
    body: 'Check your tasks!',
  },
  trigger: { seconds: 10 },
});

// Listen for received notifications
React.useEffect(() => {
  const sub = Notifications.addNotificationReceivedListener(
    (n) => console.log(n)
  );
  return () => sub.remove();
}, []);
```

---

## 26 · Deep linking

```tsx
// app.json / app.config.js
{
  "expo": {
    "scheme": "myapp"
  }
}

// Navigation linking config
const linking = {
  prefixes: ['myapp://', 'https://myapp.com'],
  config: {
    screens: {
      Home: '',
      Detail: 'detail/:id',
      Profile: 'profile',
    },
  },
};

<NavigationContainer linking={linking}>
  {/* ... */}
</NavigationContainer>

// Test: npx uri-scheme open myapp://detail/42 --android
```

---

## 27 · Animated - basic animations

```tsx
import { Animated } from 'react-native';

const opacity = React.useRef(new Animated.Value(0)).current;

// Fade in
React.useEffect(() => {
  Animated.timing(opacity, {
    toValue: 1,
    duration: 500,
    useNativeDriver: true,
  }).start();
}, []);

// Apply to component
<Animated.View style={{ opacity }}>
  <Text>Fading in…</Text>
</Animated.View>
```

Animatable with **native driver**: `opacity`, `transform` (translate, scale, rotate)

---

## 28 · Platform-specific code

```tsx
import { Platform } from 'react-native';

// Inline check
const padding = Platform.OS === 'ios' ? 44 : 24;

// Platform.select
const shadowStyle = Platform.select({
  ios: {
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.2,
    shadowRadius: 4,
  },
  android: { elevation: 4 },
});

// File-based: MyComponent.ios.tsx / MyComponent.android.tsx
// RN picks the right file automatically
```

---

## 29 · Common project structure

```
my-app/
├── App.tsx
├── src/
│   ├── components/      // reusable UI pieces
│   │   ├── Button.tsx
│   │   └── Card.tsx
│   ├── screens/         // full-page views
│   │   ├── HomeScreen.tsx
│   │   └── DetailScreen.tsx
│   ├── navigation/      // navigator setup
│   │   └── AppNavigator.tsx
│   ├── hooks/           // custom hooks
│   │   └── useFetch.ts
│   ├── services/        // API calls
│   │   └── api.ts
│   ├── store/           // global state
│   │   └── useCartStore.ts
│   └── utils/           // helpers
│       └── format.ts
├── assets/
└── app.json
```

---

## 30 · Debugging checklist

| Problem | Fix |
|---|---|
| **Red error screen** | Read the error message → fix the JS |
| **White screen** | Check console for crash → wrap in `try/catch` |
| **Metro bundler stuck** | `npx expo start --clear` |
| **Module not found** | `npx expo install <pkg>` |
| **Stale cache** | Delete `node_modules`, run `npm install` |
| **Android emulator not found** | Start emulator first, then `npx expo start` |
| **Network request failed** | Check URL, use `10.0.2.2` for Android emulator |
| **CORS error** | Does not exist in RN - check API URL |
| **Slow list** | Switch from `ScrollView` to `FlatList` |
| **State not updating** | Return a **new** object/array, not mutated one |
