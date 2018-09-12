# skip

## Specification

Controls whether to exclude a field during the serialization.

{% hint style="info" %}
Skipping a field doesn't affect the rest of its behavior \(i.e. validation\).
{% endhint %}

## Definition

```typescript
type Skip = boolean
```

**Default value:** `false`

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleFormSubmit = ({ serialized }) => {
    console.log(serialized) // { "username": "admin", "password": "123" }
  }

  render() {
    return (
      <Form action={this.handleFormSubmit}>
        <Input
          name="username"
          value="admin"
          required />
        <Input
          name="password"
          type="password"
          value="123"
          required />
        <Input
          name="confirmPassword"
          type="password"
          value="123"
          required
          skip />
      </Form>
    )
  }
}
```

