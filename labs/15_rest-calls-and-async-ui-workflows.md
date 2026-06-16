# Lab 15 - REST calls e workflow asincroni (Italian Meals App)

## Obiettivo

- Caricare **piatti italiani** da [TheMealDB](https://www.themealdb.com/api.php) con `fetch` e mostrarli in `FlatList`.
- Un solo oggetto stato con `status` (loading / error / success).
- Gestire almeno un edge case con messaggio chiaro e pulsante **Retry**.

## Timebox

2h 30m

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale
- **Lab 13–14 completati** (navigazione Lista → Dettaglio con `idMeal`)

## Scenario

Continua lo sviluppo della **Italian Meals App** (progetto finale). Dopo login e navigazione (lab 13–14), la schermata **Lista piatti** deve caricare dati reali da TheMealDB, mostrare stati UI espliciti e permettere il **Retry** in caso di errore di rete.

> **Perché questo lab:** ogni lezione 15–21 aggiunge un pezzo del **progetto finale**. Qui implementi API + stati asincroni sulla lista (e opzionalmente sul dettaglio).

## Documentazione API (consulta sempre)

- https://www.themealdb.com/documentation
- https://www.themealdb.com/api.php

| Endpoint              | URL                                                                 |
| --------------------- | ------------------------------------------------------------------- |
| Lista piatti italiani | `GET https://www.themealdb.com/api/json/v1/1/filter.php?a=Italian`  |
| Dettaglio piatto      | `GET https://www.themealdb.com/api/json/v1/1/lookup.php?i={idMeal}` |

Risposta lista: `meals[]` con `idMeal`, `strMeal`, `strMealThumb`.

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

## Cosa imparerai

1. Come incapsulare `fetch` in `services/mealsApi.ts` con controllo `res.ok`.
2. Come modellare `{ status, items, message }` in `MealsListScreen`.
3. Come riusare lo stesso pattern in `MealDetailScreen` con `{ status, meal, message }`.
4. Come mostrare `ActivityIndicator`, errore + Retry e `FlatList` di piatti.

## Passi

1. **services/mealsApi.ts** - `fetchItalianMeals` e `fetchMealById` (vedi esempio sopra).
2. **types/meal.ts** - `MealSummary`, `MealsListState`, `MealDetailState` con `LoadStatus`.
3. **MealsListScreen** - stato unico `{ status, items, message }`; funzione `loadMeals()` in `useEffect` al mount.
4. **UI condizionale** - `LoadingView` / `ErrorView` con Retry / `FlatList` con `MealCard` (thumbnail + nome).
5. **MealDetailScreen** - stesso pattern asincrono per `lookup.php`; mostra immagine, titolo, ingredienti o istruzioni.
6. **Edge case** - Simula errore (URL sbagliata o rete off) → messaggio + Retry funzionante. Lista vuota (`meals: null`) → testo «Nessun piatto italiano disponibile».

## Screenshot attesi

**Lista piatti caricata - dati da TheMealDB**

![Lab 15 - Lista piatti](../labs/imgs/lab_15_main.png)

**Stato errore - errore HTTP/rete con pulsante Retry**

![Lab 15 - Stato errore](../labs/imgs/lab_15_error.png)

**Workflow asincrono - stati loading / success / error**

![Lab 15 - Workflow asincrono](../labs/imgs/lab_15_workflow.png)

## Consegna minima

- App **Italian Meals** che parte su emulatore o device
- Lista piatti italiani da API reale
- Dettaglio piatto con fetch su `idMeal`
- Un solo stato attivo alla volta (loading / error / success)
- Retry funzionante dopo errore

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] `fetch` con controllo `res.ok` in `services/mealsApi.ts`
- [ ] Stati loading / error / success espliciti su Lista (e Dettaglio)
- [ ] Edge case gestito con messaggio chiaro
- [ ] Screenshot in Google Doc (riga **Lab 15**)

## Problemi comuni

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l'emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.
- Se l'app non si connette: controlla che PC e device siano sulla stessa rete (LAN).
- Se la lista è vuota: verifica l'URL `filter.php?a=Italian` (area con la A maiuscola).
- Se il dettaglio non carica: usa un `idMeal` dalla lista italiana (es. `52772`), non id di altre aree.

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.

## Search terms

- themealdb api react native
- fetch api react native
- react native loading state
- activityindicator flatlist
