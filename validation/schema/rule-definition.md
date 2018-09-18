# Rule definition

In React Advanced Form writing validation rules is about declaring resolver functions and applying them to a define set of fields.

## Resolver

Resolver is a function that returns the next validity of the associated field.

Resolver is explicitly analyzed aside from the rest of validation context because it is a single independent unit of validation, and should be treated as such during the composition of a validation schema.

### Definition

```typescript
type RuleResolver = (params) => boolean
```

### Parameters

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `get` | `Function` | [Reactive props](../../architecture/reactive-props.md) getter function. |
| `value` | `any` | The value of a field. |
| `fieldProps` | `Object` | Props of a field. |
| `form` | `Object` | Form component reference. |

### Resolver example

```javascript
/**
 * A simple resolver that takes the value of a field
 * and resolves when it is more than 6 characters long.
 */
const validatePassword = ({ get, value, fieldProps, form }) => {
  return value.length > 6
}
```

{% hint style="info" %}
It is a good practice to write [high-order resolvers](../../recepies/reducing-boilerplate.md). Favor functional composition.
{% endhint %}

## Selector

Selector is a key path of `[propName, propValue]` that defines the application scope of a single or multiple resolvers. The following selectors are supported:

* `type` — selects fields by their type,
* `name` — selects fields by their name.

### Example

```javascript
export default {
  type: {
    /* Each selector may accept a resolver function as a value */
    email: ({ value }) => isEmail(value),
  },
  name: {
    /* Or a map of multiple resolvers */
    vatNumber: {
      format: ({ value }) => /\d{8}/.test(value),
      checksum: ({ value }) => validateChecksum(value),
    },
  },
}
```

> INCLUDE LINK TO SELECTORS PRIORITY OF EXECUTION.

## Multiple resolvers

Each field selector can have multiple resolvers applied in parallel by accepting an Object of the shape `{[ruleName: string]: RuleResolver}` as its value.

```jsx
export default {
  type: {
    password: {
      /* Both resolvers are executed in parallel */
      capitalLetter: ({ value }) => /[A-Z]/.test(value),
      oneNumber: ({ value }) => /[0-9]/.test(value),
    },
  },
}
```

{% hint style="info" %}
Sibling resolvers are executed in parallel and are **not** exclusive.
{% endhint %}

Having unique rule names allows to associate the rule with its validation message. Using example above, we can have different error messages for `capitalLetter` and `oneNumber` rules.

\*\*\*\*[**Read more on that**](../../getting-started/validation-messages.md#specific-messages)**.**



