# serialize\(\)

## Specification

Performs a manual serialization of the current `Form`.

{% hint style="danger" %}
Invoking this manually serializes a form regardless to its validity state. This is almost never what you want. Consider using [conventional form submit](../props/action.md), which validates the fields and exposes you the serialized object.
{% endhint %}

## Definition

```typescript
type Serialize = () => Object<fieldName, fieldValue>
```

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleButtonClick = () => {
    this.form.serialize() // { "username": "admin" }
  }

  render() {
    return (
      <div>
        <Form ref={form => this.form = form}>
          <Input
            name="username"
            value="admin" />
        </Form>
        <button onClick={this.handleButtonClick}>Serialize</button>
      </div>
    )
  }
}
```

{% hint style="info" %}
You can use [`onSerialize`](../callbacks/onserialize.md) form prop to transform the serialized fields object.
{% endhint %}

