# setErrors\(\)

## Specification

Method responsible for setting the error messages to the provided fields. Accepts the delta fields object, where each field path is associated with the respective error messages. Validates any affected fields as invalid.

{% hint style="info" %}
Providing explicit `null` as error message value removes the error message, and restores the previous validity state of a field.
{% endhint %}

## Definition

```typescript
type SetErrors = (fieldsDelta: FieldsDelta) => Object

type Errors = string[] | string | null

type FieldsDelta = {
  [fieldName?]: Errors,
  [groupName?]: {
    [fieldName?]: Errors,
  },
}
```

## Examples

### On submit failure

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleRegisterFailure = ({ res, form }) => {
    const { errors } = res
    
    form.setErrors({
      username: errors.username,
      billingAddress: {
        firstName: errors.firstName,
      },
    })
  }
  
  render() {
    return (
      <Form onSubmitFailed={this.handleRegisterFailure}>
        <Input
          name="username"
          required />
        <Field.Group name="billingAddress">
          <Input
            name="firstName"
            required />
        </Field.Group>
      </Form>
    )
  }
}
```

### Form reference

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleButtonClick = () => {    
    this.formRef.setErrors({
      username: 'Error message'
    })
  }
  
  render() {
    return (
      <Form
        ref={form => this.formRef = form}
        onSubmitFailed={this.handleRegisterFailure}>
        <Input
          name="username"
          required />
        <button onClick={this.handleButtonClick}>Set error</button>
      </Form>
    )
  }
}
```

