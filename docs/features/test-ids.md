# Adding test IDs

A test ID is the name an agent, or a test, uses to find a view. Give the views that matter one and they can be found, scrolled to and tapped without guessing from their position or wording.

[← All features](../../README.md#features) · [AI agents](agent.md)

**On this page:** [Add one](#add-one) · [Names that last](#names-that-last) · [Lists](#lists) · [See what has one](#see-what-has-one) · [When there is none](#when-there-is-none)

## Add one

In React Native a test ID is the `testID` prop. Put it on the view that handles the press, not on its label:

```tsx
<Pressable testID="login-button" onPress={login}>
  <Text>Log in</Text>
</Pressable>

<TextInput testID="email-input" value={email} onChangeText={setEmail} />
```

Put it on what a person would tap, type into or read to know a screen is ready (a title, a result, an error).

## Names that last

- **Say what it is**, not where it is: `checkout-pay-button`, not `blue-button-2`.
- **Keep it when the wording changes.** A test ID does not change with copy or translation.
- **Prefix by screen** when names could repeat: `cart-total`, `profile-save`.
- **Use `-` between words**, lowercase, so every tool reads them the same.

## Lists

Give each row a test ID built from its id, so a row can be asked for by name:

```tsx
renderItem={({ item }) => (
  <Pressable testID={`order-${item.id}`} onPress={() => open(item)}>
    …
  </Pressable>
)}
```

A long list only has the rows near the screen mounted. An agent asking for `order-412` is taken there by paging through the list, and the row is scrolled into view before it is tapped.

## See what has one

Open **Dev tools → Debug → UI tree**. It lists the views on the screen by test ID, label and text, with how much of each is in view. **No test ID** lists everything that can be pressed but has none: that is your to-do list. Each row has buttons to scroll to it and to tap it, which is exactly what an agent does.

## When there is none

An agent can still ask for a view by its **text** or its **accessibility label**, but that breaks when the wording changes, and two views can share a text (it can then ask for the second one by number). Prefer a test ID.

A view cannot be found at all if it is hidden (`display: none`), outside every scroll view and off screen, or inside a WebView: the content of a WebView is not part of the React tree.
