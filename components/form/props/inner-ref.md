# innerRef

## Specification

A getter function for the actual `form` HTML element rendered by the `Form` component.

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

export default class Example extends React.Component {
  componentDidMount() {
    this.formElement // HTMLElement
  }

  render() {
    return (
      <Form innerRef={element => this.formElement = element} />
    )
  }
}
```

{% hint style="info" %}
Read more on how to reference components and elements under [Referencing](../../../architecture/referencing.md#inner-reference).
{% endhint %}

