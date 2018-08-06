---
description: Event handler called when a field acquires focus.
---

# onFocus

## Definition

```typescript
type OnFocusCallback = ({
  event: Event, // Native event reference
  fieldProps: Object|Map, // The props of the current field
  fields: Object|Map, // The state of the fields
  form: ReactComponent // Reference to the Form component
}) => void
```

## Usage

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

