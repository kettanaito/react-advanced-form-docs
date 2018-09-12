# initialValues

## Specification

An object that describes initial values of the fields.

## Definition

```typescript
type InitialValues = {
  [fieldName?: string]: any,
  [fieldGroup?: string]: {
    [fieldName?: string]: any,
  },
}
```

## Example

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class ExampleForm extends React.Component {
  render() {
    return (
      <Form initialValues={{
        username: 'admin',
        billingAddress: {
          firstName: 'John',
          lastName: 'Maverick',
        },
        deliveryAddress: {
          firstName: 'Cathaline',
          lastName: 'Sunwell',
        },
      }}>
        <Input name="username" />
        
        <Field.Group name="billingAddress">
          <Input name="firstName" />
          <Input name="lastName" />
        </Field.Group>
        
        <Field.Group name="deliveryAddress">
          <Input name="firstName" />
          <Input name="lastName" />
        </Field.Group>
      </Form>
    )
  }
}
```

{% hint style="info" %}
Field's group must also be reflected in the nesting of `initialValues` keys.
{% endhint %}

