# messages

## Specification

Form-specific validation messages.

> Providing form-specific validation messages is designed to extend/rewrite the messages applied application-wide. For general usage it is recommended to pass the validation messages to the [`FormProvider`](../../form-provider.md) component to be applied application-wide.

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

const formMessages = {
  extend: true, // merge the current messages with the FormProvider's ones
  type: {
    email: {
      invalid: 'Custom message for invalid email fields of this very form',
    },
  },
}

export default class Example extends React.Component {
  render() {
    return (
      <Form messages={formMessages}>
        {/* Fields here */}
      </Form>
    )
  }
}
```

## Materials

* [`FormProvider`](../../form-provider.md)
* [Validation messages](../../../validation/messages.md)

