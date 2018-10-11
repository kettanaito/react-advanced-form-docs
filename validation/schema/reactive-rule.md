# Reactive rule

Any validation resolver may become reactive. This means that it is being re-evaluated anytime the field prop references established in its declaration change.

## Definition

```typescript
type Get = (fieldPropPath: string[]) => any
```

## Declaration

Use `get` function from the resolver parameters to reference other fields' props.

{% code-tabs %}
{% code-tabs-item title="validation/rules.js" %}
```javascript
export default {
  name: {
    confirmPassword: ({ get, value }) => {
      return value === get(['password', 'value'])
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The resolver above marks `confirmPassword` field as valid whenever its `value` equals to the value of the `password` field. This rule is automatically re-evaluated in real time whenever the values of either fields update.

{% hint style="success" %}
Use reactive rules when the validity of a field depends on some props of another field\(s\).
{% endhint %}

