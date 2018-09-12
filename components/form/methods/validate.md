# validate\(\)

## Specification

Performs manual validation of the referenced `Form`.

{% hint style="danger" %}
Always favor conventional form submit via `Button[type="submit"]`. Form validation is obviously included prior to submit action, so there is **no need to explicitly invoke validation**. However, there are use cases to refer to manual validation. Please see those below. 
{% endhint %}

## Definition

```typescript
type Validate = () => Promise<boolean>
```

## Use cases

There are several use cases when using manual validation may be appropriate, as opposed to conventional form submit flow.

### Submitting multiple forms at once

In this case you may want to validation each form independently, and perform a submit based on the accumulated validity of all forms.

{% hint style="info" %}
Consider [`Field.Group`](../../field.group.md) for semantical separation of the form sections. Using field groups validates and submits all the groups automatically, as they are the part of a single form.
{% endhint %}

### Logic dependent on the runtime validity of a form

You may want to show/hide different UI elements, or perform any subsequent actions based on the validity of a form in the given point of time \(apart of submit\).

## Example

### Simple example

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleClick = () => {
    this.form.validate().then((isFormValid) => {
      // ...
    })
  }

  render() {
    return (
      <div>
        <Form ref={form => this.form = form}>
          <Input
            name="username"
            required />
        </Form>
        <a href="#" onClick={this.handleClick}>Validate</a>
      </div>
    )
  }
}
```

### Using async/await

Since validate function returns a Promise, you can use async/await to retrieve the validity of a form in a single line:

```javascript
handleClick = async () => {
  const isFormValid = await this.form.validate()
}
```



