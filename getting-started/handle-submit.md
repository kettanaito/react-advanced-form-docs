# Handle submit

In the end, it's all about sending the gathered data somewhere. Let's implement the most common scenario—sending the serialized form data to a remote end-point.

## Implementation

Form submit is handled by the [`action`](../components/form/props/action.md) prop provided directly to the `Form` component:

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

