# onFirstChange

## Specification

A callback function dispatched once when the first value change of a field happens.

## Parameters

| Param | Type | Description |
| :--- | :--- | :--- |
| `event` | `Event` | Change event reference. |
| `prevValue` | `any` | Previous value of the changed field. |
| `nextValue` | `any` | Next value of the changed field. |
| `fieldProps` | `Object` | Props of the field that triggered the change. |
| `fields` | `Object` | Reference to all fields in the form. |
| `form` | `Object` | Form component reference. |

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

export default class Example extends React.Component {
  handleFirstChange = ({ event, prevValue, nextValue, fieldProps, fields, form }) => {
    console.log('Field `%s` made the form dirty.', fieldProps.name)
  }

  render() {
    return (
      <Form onFirstChange={this.handleFirstChange}>
        {/* Fields here */}
      </Form>
    )
  }
}
```

