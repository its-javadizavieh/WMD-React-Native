# Lab 02 – Architettura bridge e rendering nativo

## Obiettivo

- Osserva i re-render con `console.log` e un contatore.
- Usa `FlatList` con `keyExtractor` per liste performanti.
- Gestisci almeno un edge case con un messaggio chiaro.

## Timebox

2h

## Prerequisiti

- PC con Node.js LTS installato
- VS Code e Git
- Expo oppure React Native CLI (Android)
- Android emulator oppure telefono reale

## Scenario

Costruisci una schermata con un contatore e un componente figlio `Row`. Usa `console.log` per osservare quante volte ogni componente si ri-renderizza. Poi aggiungi una `FlatList` con 20+ elementi.

> **Perché questo lab:** capire che i re-render sono normali (non un bug), e imparare a usare `FlatList` invece di `ScrollView` per liste lunghe.

## Cosa imparerai

1. Come usare `console.log` con un contatore per osservare i cicli di render.
2. La differenza tra `ScrollView` (renderizza tutto) e `FlatList` (renderizza solo il visibile).
3. Come funziona `keyExtractor` e perché serve una chiave stabile.

## Starter pattern (solo promemoria)

```tsx
let rowRenderCount = 0;

function Row({ title }: { title: string }) {
  rowRenderCount += 1;
  console.log(`Row render #${rowRenderCount} – ${title}`);
  return (
    <View style={styles.row}>
      <Text>{title}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  row: {
    padding: 12,
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    marginBottom: 8,
  },
});
```

## Passi

1. **Crea/riusa un progetto Expo** — verifica che parta su emulatore/device.
2. **SafeAreaView** — Avvolgi il contenuto con `SafeAreaView` (da `react-native`) per evitare che il testo finisca sotto la status bar.
3. **Contatore + console.log** — Aggiungi `const [count, setCount] = React.useState(0)` e un contatore `appRenderCount` con `console.log` nel corpo della funzione App.
4. **Componente Row** — Crea `Row` con un contatore `rowRenderCount` e `console.log` dentro la funzione. Aggiungi bordi con `StyleSheet` (borderWidth, borderColor, borderRadius) per rendere ogni riga visivamente distinta.
5. **FlatList** — Genera 20 elementi con `Array.from({ length: 20 }, (_, i) => ({ id: String(i+1), title: "Item " + (i+1) }))` e mostrali con `FlatList`. Usa `contentContainerStyle` per il padding della lista.
6. **Osserva i log** — Premi il pulsante e guarda quante volte App e Row si ri-renderizzano.
7. **README** — Scrivi 3-5 righe: cosa hai osservato nei log e perché succede.

## Screenshot attesi

**Lista con FlatList**

![Lab 02 - Lista con FlatList](imgs/lab_02_main.png)

**Console con re-render**

![Lab 02 - Console con re-render](imgs/lab_02_console.png)

## Consegna minima

- App che parte su emulatore o device
- UI chiara e leggibile
- Un edge case gestito con un messaggio chiaro

## Checkpoint

- [ ] Avvio progetto senza errori
- [ ] Feature completata e dimostrabile
- [ ] Edge case gestito con messaggio chiaro
- [ ] Cleanup completato

## Problemi comuni

- Se Metro non parte: chiudi processi in ascolto e riavvia `npx expo start`.
- Se l'emulatore è lento: verifica virtualizzazione/KVM/Hyper-V o usa device reale.
- Se l'app non si connette: controlla che PC e device siano sulla stessa rete (LAN).

## Cleanup

- Stoppa Metro bundler (CTRL+C).
- Chiudi emulator e libera risorse.
- Se hai usato permessi (camera/location): revoca i permessi dall'OS.
- Se hai usato storage locale: svuota i dati dell'app o rimuovi le chiavi salvate.

## Search terms

- react native rerender console.log
- flatlist keyextractor react native
- expo logs console.log
