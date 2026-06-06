# Lab 11 – Soluzione

## Cosa mostra la soluzione

- Form mobile completo con name, email, message.
- Stati di submit espliciti: idle, loading, error, success.
- `KeyboardAvoidingView` + `ScrollView` per tenere il form usabile su mobile.
- Edge case: scrivendo `error` nel messaggio si simula un errore di rete.
- Il primo tap mostra gli errori di validazione; il bottone viene disabilitato solo durante loading.

## Screenshot

![Lab 11 - Form controllato](../labs/imgs/lab_11_main.png)

![Lab 11 - Errori di validazione](../labs/imgs/lab_11_errors_1.png)

## Codice

### App.tsx

```tsx
import React from "react";
import {
  KeyboardAvoidingView,
  Platform,
  Pressable,
  ScrollView,
  StyleSheet,
  Text,
  TextInput,
} from "react-native";
import { SafeAreaProvider, SafeAreaView } from "react-native-safe-area-context";

type SubmitStatus = "idle" | "loading" | "error" | "success";

export default function App() {
  const [name, setName] = React.useState("");
  const [email, setEmail] = React.useState("");
  const [message, setMessage] = React.useState("");
  const [submitted, setSubmitted] = React.useState(false);
  const [status, setStatus] = React.useState<SubmitStatus>("idle");

  const nameOk = name.trim().length >= 2;
  const emailOk = email.includes("@");
  const shouldSimulateError = message.trim().toLowerCase().includes("error");
  const messageOk = message.trim().length >= 10 || shouldSimulateError;
  const canSubmit = nameOk && emailOk && messageOk;
  const isSending = status === "loading";

  function onSubmit() {
    setSubmitted(true);
    if (!canSubmit || isSending) return;

    setStatus("loading");

    setTimeout(() => {
      if (shouldSimulateError) {
        setStatus("error");
        return;
      }

      setStatus("success");
    }, 900);
  }

  return (
    <SafeAreaProvider>
      <SafeAreaView style={{ flex: 1 }}>
        <KeyboardAvoidingView
          style={{ flex: 1 }}
          behavior={Platform.OS === "ios" ? "padding" : undefined}
        >
          <ScrollView
            contentContainerStyle={styles.container}
            keyboardShouldPersistTaps="handled"
          >
            <Text style={styles.title}>Contact support</Text>
            <Text style={styles.helper}>
              Compila name ed email, poi scrivi `error` nel messaggio per simulare
              un submit fallito.
            </Text>

            <TextInput
              value={name}
              onChangeText={setName}
              placeholder="Name"
              style={styles.input}
            />
            {submitted && !nameOk && (
              <Text style={styles.error}>Name must have at least 2 characters</Text>
            )}

            <TextInput
              value={email}
              onChangeText={setEmail}
              placeholder="Email"
              autoCapitalize="none"
              keyboardType="email-address"
              style={styles.input}
            />
            {submitted && !emailOk && (
              <Text style={styles.error}>Email must include @</Text>
            )}

            <TextInput
              value={message}
              onChangeText={setMessage}
              placeholder="How can we help?"
              multiline
              textAlignVertical="top"
              style={[styles.input, styles.textarea]}
            />
            {submitted && !messageOk && (
              <Text style={styles.error}>Message must have at least 10 characters</Text>
            )}

            <Pressable
              onPress={onSubmit}
              disabled={isSending}
              style={[styles.button, (!canSubmit || isSending) && styles.buttonDisabled]}
            >
              <Text style={styles.buttonText}>
                {status === "loading" ? "Sending..." : "Send"}
              </Text>
            </Pressable>

            {status === "error" && (
              <Text style={styles.error}>Network request failed. Try again.</Text>
            )}
            {status === "success" && (
              <Text style={styles.success}>Request sent ✓</Text>
            )}
          </ScrollView>
        </KeyboardAvoidingView>
      </SafeAreaView>
    </SafeAreaProvider>
  );
}

const styles = StyleSheet.create({
  container: { flexGrow: 1, padding: 16, gap: 10 },
  title: { fontSize: 20, fontWeight: "600" },
  helper: { color: "#555" },
  input: { borderWidth: 1, borderRadius: 8, padding: 10 },
  textarea: { minHeight: 120 },
  button: {
    paddingVertical: 10,
    paddingHorizontal: 16,
    borderRadius: 8,
    borderWidth: 1,
    alignItems: "center",
    backgroundColor: "#007AFF",
  },
  buttonDisabled: { opacity: 0.4 },
  buttonText: { fontWeight: "600", color: "#fff" },
  error: { color: "#B00020" },
  success: { color: "#0A7F2E", fontWeight: "600" },
});
```
