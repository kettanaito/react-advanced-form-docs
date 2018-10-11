# Creating form

React Advanced form treats any form as a composition of fields. Therefore, creating a form is a trivial procedure of rendering field components as the form's children.

{% hint style="warning" %}
Make sure you have [field components defined](creating-fields.md) before proceeding with this step.
{% endhint %}

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

/* Fields */
import { Input, Checkbox } from '../fields'

export default class ExampleForm extends React.Component {
  render() {
    return (
      <Form>
        <Input
          name="userEmail"
          required />
        <Input
          name="userPassword"
          type="password"
          required />
        <Checkbox
          name="termsAndConditions" />
      </Form>
    )
  }
}
```

