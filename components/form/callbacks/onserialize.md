# onSerialize

## Specification

A callback handler dispatched upon form serialization. Accepts the original serialized fields and return the next state of serialized fields.

## Parameters

| Param name | Type | Description |
| :--- | :--- | :--- |
| `serialized` | `Object` | Original serialized fields. |
| `fields` | `Object` | Form fields. |
| `form` | `Object` | Form component reference. |

## Example

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class ExampleForm extends React.Component {
  /* Callback method accepts "raw" serialized object */
  mapSerialized = ({ serialized, fields, form }) => {
    const { password, billingAddress: { address  } = serialized
    const [_, street, houseNumber] = address.match(/(.+)(\d+)/)
    
    return {
      ...serialized,
      /* Transforms the serialized value of "password" field */
      password: btoa(password),
      
      /* Beware to preserve field group nested keys */
      billingAddress: {
        street,
        houseNumber,
      },
    }
  }
  
  /* Any subsequent handlers accept transformed "serialized" object */
  registerUser = ({ serialized, fields, form }) => {
    console.log(serialized) // { "username": "admin", "password": "..." }
  }
  
  render() {
    <Form
      action={this.registerUser}
      onSerialize={this.mapSerialized}>
      <Input
        name="username"
        label="Username"
        initialValue="admin"
        required />
      <Input
        name="password"
        label="Password"
        initialValue="foo"
        required />
      <Field.Group name="billingAddress">
        <Input
          name="address"
          initialValue="Baker st. 12" />
      </Field.Group>
    </Form>
  }
}
```

