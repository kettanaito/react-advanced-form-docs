# Controlled fields

## Favor uncontrolled

{% hint style="info" %}
This is a topic about [Controlled fields](https://reactjs.org/docs/forms.html#controlled-components).
{% endhint %}

Making something controlled comes with the expense of maintaining it. The more things you maintain, the more responsibility is delegated to your logic. This delegation is often unnecessary, making you do the job without getting the benefits out of it. Pay for what benefits you.

Most of the time people make fields controlled in order to access their value or state during certain form events \(i.e. validation, serialization, submit\). React Advanced Form is aware of those scenarios and exposes you a field's value and its entire state in the parameters of [**all** **form callback methods**](../components/form/callbacks/).

{% hint style="success" %}
React Advanced Form allows you to have controlled fields, but gives you a friendly notice that you may not need that.
{% endhint %}

## When to use controlled fields

We suggest using controlled fields when you need to have a custom logic based on a field's state that happens outside the common form events.

## Internals

### Uncontrolled update model

This model is called "uncontrolled" in regards to the end developer not being responsible for managing its value updates. Internally, all fields are controlled and stored in the `fields` map.

![Digram illustrates uncontrolled field update model.](../.gitbook/assets/raf-update-model-1.png)

### Controlled update model

Controlled field implies that the end developer provides an explicit `onChange` handler responsible for updating the data source of a field's value.

Internally, that means that a field's value is no longer updated on `handlers.handleFieldChange`, but instead it invokes a custom `onChange` handler. Since the handler updates the data source, the field component will receive the next value and catch it in `componentWillReceiveProps`. Then it emits a forced `fieldChange` event, thus distinguishing that current field change should propagate to the fields.

As you can see, even with the controlled field the only source of truth for a field's state is still an internal instance of `fields` inside the form component.

![Diagram illustrates controlled field update model.](../.gitbook/assets/raf-update-model-page-2-1.png)

## Example

Making a field controlled in React Advanced Form is the same as anywhere else: provide the `value` prop and the `onChange` handler.

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default Example extends React.Component {
  state = {
    username: 'admin',
  }
  
  handleUsernameChange = ({ nextValue }) => {
    this.setState({ username: nextValue })
  }
  
  render() {
    const { username } = this.state
    
    return (
      <Form>
        <Input
          name="username"
          value={username}
          onChange={this.handleUsernameChange}
          required />
      </Form>
    )
  }
}
```

{% hint style="info" %}
Read more on a field's [`onChange`](../components/field/callbacks/on-change.md) method and its parameters.
{% endhint %}

