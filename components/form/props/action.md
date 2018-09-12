# action

## Specification

Action performed on the successful submit of the form.

This function is called only when the form is valid.

## Definition

```typescript
type Action = (params) => Promise<any>
```

## Parameters

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `serialized` | `Object` | Serialized fields of the form. |
| `fields` | `Object` | Reference to all fields. |
| `form` | `Object` | Form component reference. |

{% hint style="info" %}
`action` function must always return a Promise.
{% endhint %}

## Example

### Simple example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class RegistrationForm extends React.Component {
  registerUser = ({ serialized, fields, form }) => {
    return fetch('https://back.end/user', {
      method: 'POST',
      body: JSON.stringify(serialized),
    })
  }

  render() {
    return (
      <Form action={this.registerUser}>
        <Input
          name="username"
          label="Username"
          required />
        <Input
          name="password"
          label="Password"
          required />
      </Form>
    )
  }
}
```

{% hint style="info" %}
You can use [`onSerialize`](../callbacks/onserialize.md) form prop to transform the serialized fields object prior to accepting them in the `action` handler.
{% endhint %}

### Example with Redux

```jsx
import React from 'react'
import { connect } from 'react-redux'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'
import { registerUser } from '@store/user/actions'

class RegistrationForm extends React.Component {
  registerUser = ({ serialized, fields, form }) => {
    return this.props.registerUser(serialized)
  }

  render() {
    return (
      <Form action={this.registerUser}>
        <Input
          name="username"
          label="Username"
          required />
        <Input
          name="password"
          label="Password"
          required />
      </Form>
    )
  }
}

export default connect(null, { registerUser })(RegistrationForm)
```

{% hint style="info" %}
You need to use a dedicated Redux middleware for the actions to return a Promise \(i.e. `redux-thunk` or `redux-saga`\).
{% endhint %}

