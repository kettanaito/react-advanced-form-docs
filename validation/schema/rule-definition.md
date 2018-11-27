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

Selector is a key path of `[propName, propValue]` that defines the application scope of a single or multiple validation resolvers. Think of it as a CSS selector, that controls which elements \(fields\) are effected by the specified rules \(validation\). The following selectors are supported:

* `type` — selects fields by their type,
* `name` — selects fields by their name.
* `fieldGroup` — selects the fields under the specified field group path.

### Priority

Selectors are executed in a certain order \(from highest to lowest\):

1. `name[fieldName]` / `name[fieldName][ruleName]`
2. `type[fieldType]` / `type[fieldType][ruleName]`

{% hint style="warning" %}
Each selector \(`name` and `type`\) is exclusive, meaning that when any of its resolvers reject, the next selector will not be called.  This does not apply to sibling rules in [multiple resolvers](rule-definition.md#multiple-resolvers).
{% endhint %}

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

{% hint style="warning" %}
Sibling resolvers are executed in parallel, and are _not_ exclusive.
{% endhint %}

Having unique rule names allows to associate the rule with its validation message. Using example above, we can have different error messages for `capitalLetter` and `oneNumber` rules.

\*\*\*\*[**Read more on that**](../../getting-started/validation-messages.md#specific-messages)**.**

## Grouped fields

Apart from less specific selectors \(type/name\), it is also possible to select fields based on their field group\(s\). Include the field groups key path in the schema as a value of the `fieldGroup` key:

```jsx
export default {
  fieldGroup: {
    billingAddress: {
      /* Same generic type/name selectors available under a group */
      type: {},
      name: {
        [...]: () => {},
      },
      /* Nested field groups are supported */
      paymentInfo: {
        name: {
          bankAccount: ({ value }) => validateBankAccount(value),
        },
      },
    },
    deliveryAddress: {
      name: {
        country: ({ value }) => isSupportedCountry(value),
      },
    },
  },
}
```

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input, Select } from './fields'
import validationRules from './validationRules'

export default class FormExample extends React.Component {
  render() {
    return (
      <Form rules={validationRules}>
        <Input name="..." />
        
        <Field.Group name="billingAddress">
          {/* Not selected in the validation schema */}
          <Select name="country">
            <option value="de">Germany</option>
            <option value="gb">United Kingdom</option>
          </Select>
            
          <Field.Group name="paymentInfo">
            <Input name="bankAccount" />
          </Field.Group>
        </Field.Group>
        
        <Field.Group name="deliveryAddress">
          <Select name="country">
            <option value="de">Germany</option>
            <option value="gb">United Kingdom</option>
          </Select>
        </Field.Group>
      </Form>
    )
  }
}
```

{% hint style="info" %}
Learn more about [Field grouping](../../components/field-group.md).
{% endhint %}



