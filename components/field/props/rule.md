# rule

## Specification

A synchronous rule applied to the field as the top priority validation. When the `rule` rejects, all the remaining validation chain is ignored.

## Definition

```typescript
type Rule = RegExp | (params) => boolean
```

## Parameters

The following parameters are exposed to the `rule` when it is a function:

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `get` |  |  |
| `value` | `any` | The current value of the field. |
| `fieldProps` | `Object` | Props of the current field. |
| `fields` | `Object` | Map of all fields. |
| `form` | `Object` | A reference to the current `Form` |

## Example

### Regular expression

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        <Input
          name="username"
          rule={/^\d+/} />
      </Form>
    )
  }
}
```

### Resolver function

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  validateUsername = ({ get, value, fieldProps, fields, form }) => {
    /* "username" is valid only when equals to "foo" */
    return value === 'foo'
  }
  
  render() {
    return (
      <Form>
        <Input
          name="username"
          rule={this.validateUsername} />
      </Form>
    )
  }
}
```

### Reactive rule

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        <Input
          name="password"
          type="password"
          required />
        <Input
          name="confirmPassword"
          rule={({ get, value }) => {
            /* Valid only when equals to "password" field's value */
            return value === get(['password', 'value'])
          }}
          required />
      </Form>
    )
  }
}
```

{% hint style="info" %}
Read more about [Reactive props](../../../architecture/reactive-props.md) feature, it is a game-changer.
{% endhint %}

