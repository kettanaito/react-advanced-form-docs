# Creating form

React Advanced form treats any form as a composition of fields. Therefore, creating a form is a trivial procedure of rendering [field components](creating-fields.md) as the `<Form/>`'s children. Make sure you have field components defined before proceeding with this step.

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

/* Composite field components */
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

> Note that this is a minimal example. More complex topics like validation or submit handling are described in the next steps of this guide. Take things one at a time.

