# Reactive rule

## Reactive resolver

There is a `get` argument exposed in each rule resolver function. It allows to reference another fields of the same form, and base the validation logic on their state.

Whenever a field is referenced in a resolver, the latter is automatically called each time the referenced field's prop update. Consider the following example:

```javascript
{
  name: {
    confirmPassword: ({ get, value }) => {
      return (value === get(['password', 'value'])
    }
  }
}
```

Based on the declaration above, a `[name="confirmPassword"]` field is valid when its `value` equals to the `value` prop of the `[name="password"]` sibling field. By referencing another field, `confirmPassword` field is re-validated _each time_ when the `value` prop of `password` field updates.

