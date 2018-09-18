# Form

## Specification

Component that wraps the set of fields and controls their data flow.

The key focus of a form design is getting rid of obscure configurations and achieving a clear and predictable layout. Although depending on the use case, form shares a lot of functionalities and behaviors. Unifying the latter, depriving the developer from configuring it over and over, is a primary goal of React Advanced Form.

## Props

### General

| Prop name | Type | Description |
| :--- | :--- | :--- |
| `ref` | `Function` | Getter function for the `<Form>` component. |
| [`innerRef`](props/innerref.md) | `Function` | Getter function for the `form` element. |
| [`action`](props/action.md) | `Function<Promise>` | Submit action handler. |
| [`rules`](props/rules.md) | [`ValidationRules`]() | Form-specific validation rules. |
| [`messages`](props/messages.md) | [`ValidationMessages`](../../validation/messages.md) | Form-specific validation messages. |

### Callbacks

| Callback name | Descripton |
| :--- | :--- |
| `onFirstChange` | Called when the form becomes dirty. |
| `onReset` | Called after the form has been reset. |
| `onSubmitStart` | Called when the submit has started \(form is valid\). |
| `onSubmitted` | Called after successful submit. |
| `onSubmitFailed` | Called on failed submit. |
| `onSubmitEnd` | Called when the submit has ended, regardless of its status. |
| `onInvalid` | Called when the submit failed due to form being invalid. |

{% hint style="info" %}
Read more about each prop and callback under [Form callbacks](https://redd.gitbook.io/react-advanced-form/components/form/callbacks).
{% endhint %}

## Methods

Form methods are available under its [reference](../../architecture/referencing.md#component-reference) object.

| Method name | Type | Descripton |
| :--- | :--- | :--- |
| [`validate`](methods/validate.md) | `Function<Promise>` | Validates form manually. |
| [`serialize`](methods/serialize.md) | `Function<Object>` | Serializes form manually. |
| [`reset`](methods/reset.md) | `Function` | Resets the fields to their initial values. |
| [`submit`](methods/submit.md) | `Function<Promise>` | Submits the form manually. |

{% hint style="info" %}
Learn more about each method under [Form methods](https://redd.gitbook.io/react-advanced-form/components/form/methods).
{% endhint %}

## Example

Let's create a simple form that has a single input and an action handler.

> React Advanced Form is field-centric. That means that you may want to configure a set of [composite field components](../../getting-started/creating-fields.md) as the first step of integrating this solution into your application.

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  registerUser = ({ serialized, fields, form }) => {
    console.log(serialized) // { "firstName": "John" }
  }
  
  render() {
    return (
      <Form action={this.registerUser}>
        <Input
          name="firstName"
          label="First name"
          rule={/[a-zA-Z]/}
          initialValue="John"
          required />
      </Form>
    )
  }
}
```

{% hint style="info" %}
You can use [`FormProvider`](../form-provider.md) to specify application-wide validation rules and messages, or you can pass them to a specific Form using [`rules`](props/rules.md) and [`messages`](props/messages.md) props respectively.
{% endhint %}



