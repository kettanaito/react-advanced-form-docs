# reset\(\)

## Specification

Resets the values of the unctronolled fields of the `Form` to their initial values.

> **Note:** `Form.reset()` will not affect controlled fields. To reset the latter use [`Form.onReset`](https://github.com/kettanaito/react-advanced-form/tree/75c444924d87ca8ff76bc096231173e42e717adc/docs/components/callbacks/Form/onReset.md) callback method handler, which is called after `Form.reset()` is finished.

## Usage

### Using submit callback handlers

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleSubmitted = ({ res, fields, form }) => {
    form.reset() // resets "username" field to "admin"
  }

  render() {
    return (
      <Form onSubmitted={this.handleSubmitted}>
        <Input
          name="username"
          initialValue="admin" />
      </Form>
    )
  }
}
```

### Using form reference

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class MyForm extends React.Component {
  handleButtonClick = () => {
    this.form.reset() // resets "username" field to "admin"
  }

  render() {
    return (
      <Form ref={form => this.form = form}>
        <Input
          name="username"
          initialValue="admin" />
        <button onClick={this.handleButtonClick}>Reset</button>
      </Form>
    )
  }
}
```

### Reset controlled fields

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class MyForm extends React.Component {
  state = {
    username: 'foo'
  }
  
  handleUsernameChange = ({ nextValue }) => {
    this.setState({ username: nextValue })
  }
  
  resetForm = () => {
    this.setState({ username: '' })
  }
    
  render() {
    const { username } = this.state
        
    return (
      <Form onReset={this.resetForm}>
        <Input
          name="username"
          value={username}
          onChange={this.handleUsernameChange} />
      <Form>
    )
  }
}
```

