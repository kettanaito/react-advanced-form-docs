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

## Priority

There are multiple way to affect initial value of a field. The first value found in the list below will be used as the initial value for a field \(sorted by priority\):

1. `Form.props.initialValues`
2. `Field.props.initialValue`
3. `FieldClass.initialValue`

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

