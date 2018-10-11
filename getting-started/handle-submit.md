# Handle submit

Provide the [`action`](../components/form/props/action.md) prop to handle a submit of a `Form` component.

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

export default class ExampleForm extends React.Component {
  render() {
    return (
      <Form action={this.registerUser}>
        {/* ... */}
      </Form>
    )
  }
}
```

The `action` prop expects a function which returns a Promise. By returning the latter Form can properly react to the Promise status, which is a submit request status at the same time.

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

export default class ExampleForm extends React.Component {
  registerUser = ({ serialized, fields, form }) => {
    return fetch(API_URL, {
      method: 'POST',
      body: JSON.stringify(serialized),
    })
  }

  render() {
    return (
      <Form action={this.registerUser}>
        {/* ... */}
      </Form>
    )
  }
}
```

{% hint style="info" %}
Read more about the [`action`](../components/form/props/action.md) prop.
{% endhint %}

