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

## Screenshot

**Stesso stato empty del lab 04, ma con codice separato**

![Lab 05 - Stato empty](../labs/imgs/lab_04_empty.png)

**Una nota aggiunta dopo il refactor modulare**

![Lab 05 - Una nota aggiunta](../labs/imgs/lab_04_success_1.png)

**Struttura cartelle - components / screens / services**

![Lab 05 - Struttura cartelle](../labs/imgs/lab_05_structure.png)
