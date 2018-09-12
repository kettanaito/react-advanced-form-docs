# Rule definition

## Resolvers

Resolver is a function that returns the next validity of the associated field.

Resolver is explicitly analyzed apart from the rest validation context because it is a single independent unit of validation and should be treated as such during the composition of a validation schema.

### Definition

```typescript
type RuleResolver = (params) => boolean
```

### Parameters

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `get` | `Function` | ... |
| `value` | `any` | The value of a field. |
| `fieldProps` | `Object` | Props of the current field. |
| `fields` | `Object` | Reference to all fields of a form. |
| `form` | `Object` | Form component reference. |

### Resolver example

```javascript
/**
 * A simple resolver that takes the value of a field
 * and resolves when it is more than 6 characters long.
 */
const validatePassword = ({ get, value, fieldProps, fields, form }) => {
  return value.length > 6
}
```

{% hint style="info" %}
It is a good practice to write [high-order resolvers](../../recepies/reducing-boilerplate.md). Favor functional composition.
{% endhint %}

## Selectors

Validation is about applying resolvers to the selected field\(s\). It is possible to select the fields based on the next selectors:

* `type` — selects fields by their type
* `name` — selects field by its name

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

## Multiple rules

Each field selector can accept multiple resolvers to be applied in parallel. To do so, pass an Object with the shape `{ [ruleName: string]: ResolverFunction }` as a value of that selector.

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
Sibling resolvers execute in parallel and are **not** exclusive.
{% endhint %}

Including unique rule name allows to associate the rule with its validation message. Using example above, we can have different error messages for `capitalLetter` and `oneNumber` rules.

\*\*\*\*[**Read more on that**](../../getting-started/validation-messages.md#specific-messages)**.**



