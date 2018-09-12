# onFocus

## Specification

Event handler called when a field acquires focus.

## Definition

```typescript
type OnFocus = (params) => void
```

## Parameters

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `event` | `Event` | Native event reference. |
| `fieldProps` | `Object` | Props of the current field. |
| `fields` | `Object` | Reference to all fields of a form. |
| `form` | `Object` | Form component reference. |

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleUsernameFocus = ({ event, fieldProps, fields, form }) => {
    // ...
  }

  render() {
    return (
      <Form>
        <Input
          name="username"
          onFocus={this.handleUsernameFocus}
          required />
      </Form>
    )
  }
}
```

