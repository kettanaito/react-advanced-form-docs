# Creating form

## Introduction

React Advanced Form is field-centric. That means that it treats each form as a composite component containing various [field components](https://github.com/kettanaito/react-advanced-form/tree/75c444924d87ca8ff76bc096231173e42e717adc/docs/getting-started/creating-fields/README.md).

## Implementation

1. Import and use a `<Form>` component directly from `react-advanced-form` library.
2. Use necessary field components as the children of the form, no matter the depth or nature \(static/dynamic\).

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

> Note that this is a minimal example. More complex topics like validation or submit handling are described in the next steps of this guide. Taking things one at a time is a key to understanding.

