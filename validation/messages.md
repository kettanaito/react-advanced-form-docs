# Validation messages

## Specification

Validation messages reside in the separate schema, decoupled from the validation logic. The reasons for the decoupling are the following:

* Establish a clear separation of concerns.
* Prevent from garbaging complex validation rules with the messages.
* Have a single validation schema associated with any amount of localized messages schema.

## Resolver

Any message can be a plain string, or a resolver function that returns a string.

Resolvers are useful when a validation message derives not only from the field's validity, but also from its state, fields or a form. This way you can include the current value of a field in the error message, for example.

### Definition

```typescript
type MessageResolver = string | (params) => string
```

### Parameters

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `value` | `any` | The value of a field. |
| `fieldProps` | `Object` | Props of a field. |
| `fields` | `Object` | State of all fields. |
| `form` | `Object` | Form component reference. |
| `extra` | `Object` | Extra parameters passed in the async validation payload. |

## Message types

Validation messages schema supports the following message types:

| Type | Description |
| :--- | :--- |
| `missing` | A message for an empty required field. |
| `invalid` | A message for an invalid field. |
| `async` | A message corresponding to the invalid [asynchronous validation](../components/field/props/async-rule.md). |

## Selectors

Selectors are used to associate [message resolvers](messages.md#resolvers) to the relevant field\(s\).

| Selector | Description |
| :--- | :--- |
| `name` | Name-specific messages. |
| `type` | Type-specific messages. |
| `general` | General messages. Those are used as fallback values in case more specific messages are not present. |

Each selector expects the map of the selector values and its [resolvers](messages.md#resolvers):

```typescript
type ValidationMessages = {
    [selectorValue: string]: MessageResolver,
  },
}
```

## Named resolvers

It is possible to associate validation rules with the specific validation messages. To do that, provide the `{ ruleName: message }` map as the value of the `rule` key in the respective selector:

```javascript
export default {
  type: {
    password: {
      missing: 'Please provide the password',
      invalid: 'The passwords is invalid',
      rule: {
        minLength: 'Password must be at least 6 characters long',
      },
    },
  },
}
```

> **Note:** Named resolver must have the corresponding validation rule with the same name in order to resolve. Otherwise, the closest validation message will be returned by the resolver. Considering the example above, if `minLength` rule doesn't exist and the `type=["password"]` field is invalid, the closest `invalid` resolver will be used \(which is `type.password.invalid` in this case\).

## Fallbacks

Whenever the resolver cannot resolve it would attempt to grab the closest resolver recursively and resolve it instead. Fallback resolvers are iterated by their specificity, which can be presented as follows:

### Fallback sequence

Here is the resolver paths \(listed by priority, from highest to lowest\):

1. `messages.name[fieldName][ruleName]`
2. `messages.name[fieldName].invalid` / `messages.name[fieldName].missing`
3. `messages.type[fieldType][ruleName]`
4. `messages.type[fieldType]invalid` / `messages.type[fieldType].missing`
5. `messages.general.invalid` / `messages.general.missing`

### Example

Consider the following validation messages:

```javascript
export default {
  general: {
    invalid: 'General invalid message',
  },
  type: {
    email: {
      invalid: 'E-mail is invalid',
    },
  },
  name: {
    userEmail: {
      invalid: 'User e-mail is invalid',
      rule: {
        includesAt: 'E-mail must include "@" character',
      },
    },
  },
}
```

And the following component layout:

```jsx
<Form>
  <Input
    type="email"
    name="userEmail"
    value="foo" />
</Form>
```

With the given scenario the `includesAt` validation rule would reject, marking the field as unexpected. This must be reflected in the UI using the validation messages schema.

This is the priority sequence in which resolvers will attempt to resolve the validation message:

1. `name.userEmail.rule.includesAt`
2. `name.userEmail.invalid`
3. `type.email.invalid`
4. `general.invalid`

The validation message resolves as soon as the resolver returns the value. The same sequence applies for the type-specific named resolvers.



