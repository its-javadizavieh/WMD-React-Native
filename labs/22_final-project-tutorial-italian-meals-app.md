# Progetto finale - Tutorial: Italian Meals App

## Obiettivo

Realizzare un'app **Expo/React Native** individuale che integra le competenze delle **lezioni 1–19** (laboratori 01–19). L'app mostra **piatti italiani** da [TheMealDB](https://www.themealdb.com/), con **login mock**, navigazione, API, preferiti persistiti, stato globale, UI responsive e accessibilità.

Le **lezioni 20–21** (feature native, notifiche) sono **opzionali**: implementale solo se sei in grado.

**Soluzioni di riferimento (lab 01–21):** [GitHub - lab_solutions](https://github.com/its-javadizavieh/WMD-React-Native/tree/main/lab_solutions)

Riusa componenti e pattern già visti nei laboratori - **non ripartire da zero**.

## Scadenze

| Fase                | Quando                                          | Cosa consegnare                                                                                       |
| ------------------- | ----------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Checkpoint**      | **9 luglio 2026**                               | Repository sul tuo **GitHub** + file **`PROGRESS.md`** con **screenshot** di ogni schermata richiesta |
| **Consegna finale** | **Fine del quarto semestre** (data da definire) | Link repo su **FAD** + **README** completo                                                            |

Sviluppo **take-home** (a casa), con commit consigliati **ogni settimana**.

---

## Documentazione API (obbligatoria da consultare)

- **Documentazione generale:** https://www.themealdb.com/documentation
- **Riferimento endpoint:** https://www.themealdb.com/api.php

L'API è **gratuita** per uso didattico. Test key: `1` (già nell'URL sotto).

---

## Scenario

**Italian Meals App** - dopo il login, l'utente vede **avatar rotondo + nome** (come nel **lab 07**), poi la lista di piatti italiani, apre il dettaglio (ricetta, ingredienti, immagine), aggiunge preferiti, cerca/filtra, e gestisce impostazioni (es. logout, tema).

Usa i tuoi lab precedenti come mattoni - e le [soluzioni su GitHub](https://github.com/its-javadizavieh/WMD-React-Native/tree/main/lab_solutions) come riferimento.

---

## Schermate obbligatorie (checkpoint 9 luglio)

Ogni schermata deve avere uno **screenshot** in `PROGRESS.md`.

| #   | Schermata            | Cosa deve mostrare                                                                                                                                                               |
| --- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Login**            | Form controllato; accesso solo con credenziali mock valide; messaggio errore se credenziali sbagliate                                                                            |
| 2   | **Header profilo**   | Dopo login: **avatar rotondo** (`Image` in contenitore con `borderRadius` + `overflow: hidden`) e **nome** utente loggato (pattern **lab 07**); visibile in lista o impostazioni |
| 3   | **Lista piatti**     | `FlatList` da API italiana; `loading` / `error` / `success` (e `empty` se applicabile)                                                                                           |
| 4   | **Ricerca / filtro** | Campo testo che filtra la lista (form controllato, lab 07–11)                                                                                                                    |
| 5   | **Dettaglio**        | Dati da `lookup.php?i={idMeal}`; immagine, titolo, istruzioni o ingredienti                                                                                                      |
| 6   | **Preferiti**        | Toggle preferito; persistenza **AsyncStorage** (`app:v1:favs`)                                                                                                                   |
| 7   | **Impostazioni**     | Logout (torna al login); avatar + nome utente; eventuale tema                                                                                                                    |
| 8   | **Stato errore**     | Screenshot con errore rete/API + pulsante **Retry**                                                                                                                              |
| 9   | **Accessibilità**    | Almeno 2 accorgimenti visibili (es. `accessibilityLabel` su pulsanti/card)                                                                                                       |

---

## Login mock - 3 utenti

L'autenticazione è **solo locale** (nessuna API di login). Confronta email/username e password con un array mock in `services/auth.ts` (o simile).

| Utente | Email                       | Password      |
| ------ | --------------------------- | ------------- |
| 1      | `mario.rossi@student.it`    | `React2026!`  |
| 2      | `giulia.bianchi@student.it` | `Expo2026!`   |
| 3      | `luca.verdi@student.it`     | `Mobile2026!` |

**Array da usare in `services/auth.ts`:**

```ts
// services/auth.ts
export const MOCK_USERS = [
  {
    email: "mario.rossi@student.it",
    password: "React2026!",
    name: "Mario Rossi",
    avatarUri: "https://picsum.photos/seed/mario-rossi/128",
  },
  {
    email: "giulia.bianchi@student.it",
    password: "Expo2026!",
    name: "Giulia Bianchi",
    avatarUri: "https://picsum.photos/seed/giulia-bianchi/128",
  },
  {
    email: "luca.verdi@student.it",
    password: "Mobile2026!",
    name: "Luca Verdi",
    avatarUri: "https://picsum.photos/seed/luca-verdi/128",
  },
];

export function validateLogin(email: string, password: string) {
  return MOCK_USERS.find(
    (u) => u.email === email.trim() && u.password === password,
  );
}
```

**Comportamento atteso:**

- Credenziali corrette → salva sessione (utente con `name` e `avatarUri`) → naviga alla **Lista**
- Credenziali errate → `setError("Email o password non validi")` senza crash
- **Logout** da Impostazioni → cancella sessione → torna al **Login**

> Pattern lab 11: input controllati, validazione, feedback errore.

### Avatar utente (lab 07)

Dopo il login mostra **avatar rotondo** e **nome** dell'utente autenticato (in header della lista, in impostazioni, o in entrambi). Riusa il pattern del lab 07: `Image` dentro un `View` con `borderRadius` e `overflow: "hidden"`.

```tsx
// components/Avatar.tsx - adattato da lab 07
function Avatar({ uri, size = 48 }: { uri: string; size?: number }) {
  const [failed, setFailed] = React.useState(false);
  const radius = size / 2;

  return (
    <View
      style={{
        width: size,
        height: size,
        borderRadius: radius,
        overflow: "hidden",
        borderWidth: 1,
      }}
    >
      {failed ? (
        <Text style={{ textAlign: "center", lineHeight: size }}>?</Text>
      ) : (
        <Image
          source={{ uri }}
          style={{ width: size, height: size }}
          onError={() => setFailed(true)}
          accessibilityLabel="Avatar utente"
        />
      )}
    </View>
  );
}
```

Esempio header dopo login:

```tsx
<View style={{ flexDirection: "row", alignItems: "center", gap: 12 }}>
  <Avatar uri={user.avatarUri} />
  <Text>{user.name}</Text>
</View>
```

Riferimento completo: [soluzione lab 07](https://github.com/its-javadizavieh/WMD-React-Native/blob/main/lab_solutions/07_solution-react-native-base-components-part-1.md).

---

## API TheMealDB - lista → dettaglio

### Lista piatti italiani

```
GET https://www.themealdb.com/api/json/v1/1/filter.php?a=Italian
```

Risposta: `meals[]` con `idMeal`, `strMeal`, `strMealThumb`.

### Dettaglio per id

```
GET https://www.themealdb.com/api/json/v1/1/lookup.php?i={idMeal}
```

Risposta: `meals[0]` con `strMeal`, `strCategory`, `strArea`, `strInstructions`, `strMealThumb`, ingredienti (`strIngredient1`… `strMeasure1`…).

Usa sempre un **`idMeal` dalla lista italiana** (es. `52961`, `52796`, `52839`), non id di altre aree.

### Esempio fetch (`services/mealsApi.ts`)

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

### Retry (lab 15–16)

In caso di errore di rete, riprova al massimo **2 volte** prima di mostrare lo stato `error` con pulsante **Riprova**.

---

## Architettura consigliata

```
src/
  components/     MealCard, Avatar, LoadingView, ErrorView
  screens/        LoginScreen, MealsListScreen, MealDetailScreen, SettingsScreen
  navigation/     Auth stack + App stack (React Navigation)
  services/       mealsApi.ts, auth.ts, storage.ts
  context/        AuthContext, FavoritesContext (o Zustand)
  theme/          colori, spacing
App.tsx
PROGRESS.md       checkpoint 9 luglio
README.md         consegna finale
docs/screenshots/ immagini per PROGRESS.md
```

**Regola:** fetch e logica dati in `services/`, non nel JSX presentazionale (lab 05, 15).

---

## Roadmap - lezioni 1–19

### Lab 01–03 - Setup, componenti, props, eventi

- Progetto Expo funzionante (`npx expo start`)
- Componenti base: `MealCard`, `PrimaryButton`, layout con `View` / `Text`

### Lab 04–06 - Architettura modulare

- Separa `screens/`, `components/`, `services/` (lab 05)
- Nessuna logica API dentro il JSX presentazionale

### Lab 07–11 - State e form

- **Avatar:** `Image` rotondo con fallback `?` su errore (lab 07)
- **Login:** `useState` per email/password; form controllato
- **Header profilo:** dopo login, avatar + nome utente dalla sessione
- **Ricerca lista:** `TextInput` controllato che filtra `meals` in memoria

### Lab 09–10 - useEffect

- Carica lista in `useEffect` al mount della schermata Lista
- Carica dettaglio in `useEffect` quando cambia `idMeal` (param route)
- Cleanup se serve (cancel flag / abort)

### Lab 13–14 - Navigazione

- **Auth flow:** stack Login → (dopo login) stack principale
- **App stack:** Lista → Dettaglio (`params: { idMeal }`) → Impostazioni
- Tipizzare i param con TypeScript se possibile

### Lab 15–16 - REST e stati UI

- Un oggetto stato: `{ status: 'idle'|'loading'|'error'|'success', data, message }`
- `ActivityIndicator`, messaggio errore, **Retry**

### Lab 16–17 - AsyncStorage

- Chiave preferiti: `app:v1:favs` → array di `idMeal`
- Carica preferiti all'avvio; sincronizza con UI (cuore / icona)

### Lab 17–18 - Stato globale

- **Context** o **Zustand** per: utente loggato, lista preferiti, eventuale tema
- Nel README: perché hai scelto quel pattern (2–3 righe)

### Lab 18–19 - Stile, accessibilità, animazione

- `StyleSheet.create`, Flexbox, layout che funziona su schermi diversi
- `accessibilityLabel` su card e pulsanti; contrasto leggibile
- Piccola animazione (es. `opacity` fade-in sulla lista o feedback `Pressable`)

---

## Opzionale - lezioni 20–21

Non richiesto per il **9 luglio**. Se implementi:

- **Lab 20:** camera o geolocalizzazione con permessi + fallback
- **Lab 21:** notifica locale (es. promemoria “hai 3 preferiti”) - documenta limiti emulator

---

## File `PROGRESS.md` (checkpoint 9 luglio)

Crea questo file nella **root** del repository e aggiornalo fino al 9 luglio.

```md
# Progress - Italian Meals App

**Studente:** Nome Cognome  
**Repo:** https://github.com/tuo-utente/italian-meals-app  
**Ultimo aggiornamento:** YYYY-MM-DD

## Schermate implementate

| Schermata      | Stato   | Screenshot                                          |
| -------------- | ------- | --------------------------------------------------- |
| Login          | ✅ / 🚧 | ![Login](./docs/screenshots/01-login.png)           |
| Header profilo |         | ![Profilo](./docs/screenshots/02-profile.png)       |
| Lista piatti   |         | ![Lista](./docs/screenshots/03-list.png)            |
| Ricerca        |         | ![Ricerca](./docs/screenshots/04-search.png)        |
| Dettaglio      |         | ![Dettaglio](./docs/screenshots/05-detail.png)      |
| Preferiti      |         | ![Preferiti](./docs/screenshots/06-favorites.png)   |
| Impostazioni   |         | ![Impostazioni](./docs/screenshots/07-settings.png) |
| Errore + Retry |         | ![Errore](./docs/screenshots/08-error.png)          |

## Note

- Cosa manca per la consegna finale:
- Scelta stato globale:

## Utenti mock (login di test)

| Email                     | Password    |
| ------------------------- | ----------- |
| mario.rossi@student.it    | React2026!  |
| giulia.bianchi@student.it | Expo2026!   |
| luca.verdi@student.it     | Mobile2026! |
```

Salva le immagini in `docs/screenshots/` (o cartella equivalente) e referenziale nel markdown.

---

## README (consegna finale)

Per la **consegna finale** (fine del quarto semestre), il `README.md` deve includere:

- Nome progetto e autore
- **Come avviare:** `npm install`, `npx expo start`
- Endpoint API usati (link documentazione TheMealDB)
- Utenti mock per test login (tabella sopra)
- Scelta stato globale e motivazione
- Edge case gestiti (rete, login fallito, lista vuota, preferiti)
- Eventuali feature opzionali 20–21

---

## Checklist checkpoint (9 luglio)

- [ ] Repository su **GitHub** (tuo account)
- [ ] App avvia con `npx expo start` senza errori
- [ ] **Login** funziona con i **3 utenti mock**
- [ ] Dopo login: **avatar rotondo** + **nome** utente visibili (lab 07)
- [ ] Lista piatti da API **italiana** con stati loading/error/success
- [ ] Dettaglio con `lookup.php?i=`
- [ ] **Ricerca** sulla lista
- [ ] **Preferiti** in AsyncStorage (`app:v1:favs`)
- [ ] Navigazione Lista → Dettaglio → Impostazioni + **logout**
- [ ] **Retry** su errore API
- [ ] Stato globale (Context/Zustand) per sessione o preferiti
- [ ] Almeno **2** accorgimenti accessibilità
- [ ] File **`PROGRESS.md`** con **tutti gli screenshot** richiesti

---

## Checklist consegna finale (fine semestre 4)

- [ ] Tutto quanto sopra, rifinito e documentato
- [ ] Link repository caricato su **FAD**
- [ ] **README** completo
- [ ] (Opzionale) notifiche o feature native lezioni 20–21

---

## Link utili

| Risorsa                    | URL                                                                                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Tutorial progetto          | [GitHub - tutorial](https://github.com/its-javadizavieh/WMD-React-Native/blob/main/labs/22_final-project-tutorial-italian-meals-app.md) |
| Regolamento esame (30 pt)  | [FAD - Verifica finale](https://fad.its-ictpiemonte.it/course/view.php?id=2481#section-24)                                              |
| Soluzioni lab (GitHub)     | [GitHub - lab_solutions](https://github.com/its-javadizavieh/WMD-React-Native/tree/main/lab_solutions)                                  |
| TheMealDB - documentazione | https://www.themealdb.com/documentation                                                                                                 |
| TheMealDB - API            | https://www.themealdb.com/api.php                                                                                                       |
| Expo                       | https://docs.expo.dev/                                                                                                                  |
| React Navigation           | https://reactnavigation.org/docs/getting-started                                                                                        |
| AsyncStorage (Expo)        | https://docs.expo.dev/versions/latest/sdk/async-storage/                                                                                |

**Regolamento esame e punteggio (30 pt):** [FAD - Verifica finale](https://fad.its-ictpiemonte.it/course/view.php?id=2481#section-24)

---

## Problemi comuni

- **Lista vuota:** verifica URL `filter.php?a=Italian` e che `meals` non sia `null`
- **Dettaglio non carica:** controlla che `idMeal` arrivi dai `route.params`
- **Login sempre fallisce:** confronto case-sensitive su email/password; trim sugli input
- **Preferiti persi al riavvio:** verifica `AsyncStorage.setItem` / `getItem` e chiave `app:v1:favs`
- **Metro non parte:** `npx expo start -c`

---

_Tutorial progetto finale - WMD React Native - aggiornato giugno 2026_
