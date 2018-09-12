---
description: Event handler called when a field loses focus.
---

# onChange

## Specification

Event handler called on each field value change.

## Definition

```typescript
type OnChange = (params) => void
```

## Parameters

| Parameter name | Type | Description |
| :--- | :--- | :--- |
| `event` | `Event` | Native event reference. |
| `prevValue` | `any` | The previous value of a field. |
| `nextValue` | `any` | The next value of a field. |
| `fieldProps` | `Object` | Props of the current field. |
| `fields` | `Object` | Reference to all fields of a form. |
| `form` | `Object` | Form component reference. |

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleUsernameChange = ({
    event,
    nextValue,
    prevValue,
    fieldProps,
    fields,
    form
  }) => {
    // ...
  }

  render() {
    return (
      <Form>
        <Input
          name="username"
          onChange={this.handleUsernameChange}
          required />
      </Form>
    )
  }
}
```

