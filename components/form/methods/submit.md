# submit\(\)

## Specification

Performs a manual submit of the current `Form`. Submit function returns a Promise that resolves into different `SubmitState`.

{% hint style="danger" %}
Manual submit is meant for explicit usage scenarios, and is not a [conventional way](../props/action.md) of submitting your forms. If you are not sure if you need manual submit, then you don't need it.
{% endhint %}

## Definition

```typescript
type Submit = () => Promise<SubmitState>
```

## Example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
 handleSubmit = () => {
   // Make sure to return a Promise here
  }

  handleClick = () => {
    this.form.submit().then((submitState) => {
      // This is called after the Promise of `this.handleSubmit` resolves/rejects
    })
  }

  render() {
    return (
      <div>
        <Form
          ref={form => this.form = form}
          action={this.handleSubmit}>
          <Input
            name="username"
            required />
        </Form>

        <a href="#" onClick={this.handleClick}>Submit manually</a>
      </div>
    )
  }
}
```

{% hint style="info" %}
Make sure to provide `Form.props.action` since that will be invoked after calling manual submit of the form.
{% endhint %}

