# Form

## Specification

Component that wraps the set of fields and controls their data flow.

The key focus of a form design is getting rid of obscure configurations and achieving a clear and predictable layout. Although depending on the use case, form shares a lot of functionalities and behaviors. Unifying the latter, depriving the developer from configuring it over and over, is a primary goal of React Advanced Form.

## Props

### General

| Prop name | Type | Descripton |
| :--- | :--- | :--- |
| `ref` | `Function` | Getter for the `<Form>` component. |
| [`innerRef`](props/innerref.md) | `Function` | Getter for the `form` element. |
| [`action`](props/action.md) | `Function<Promise>` | Submit action handler. |
| [`rules`](props/rules.md) | [`ValidationRules`](../../validation/rules.md) | Form-specific validation rules. |
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

Read more about each prop and callback under [Form callbacks](https://redd.gitbook.io/react-advanced-form/components/form/callbacks).

## Methods

| Method name | Type | Descripton |
| :--- | :--- | :--- |
| [`validate`](methods/validate.md) | `Function<Promise>` | Validates the form manually. |
| [`serialize`](methods/serialize.md) | `Function<Object>` | Serializes the form manually. |
| [`reset`](methods/reset.md) | `Function` | Resets the fields to their initial values. |
| [`submit`](methods/submit.md) | `Function<Promise>` | Submits the form manually. |

Read more about each method under [Form methods](https://redd.gitbook.io/react-advanced-form/components/form/methods).

## Declaration

Declaring a new form using React Advanced Form doesn't require you to configure anything, just render a `Form` component and its children [Fields](https://redd.gitbook.io/react-advanced-form/getting-started/creating-fields).

```jsx
import React from 'react';
import { Form } from 'react-advanced-form';

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        { /* Fields here */ }
      </Form>
    );
  }
}
```

> **Note:** Also placing a `Form` component is enough to create an isolated form, it is recommended to use the [FormProvider](../formprovider.md) to ensure unified behavior of the forms throughout the whole application.

