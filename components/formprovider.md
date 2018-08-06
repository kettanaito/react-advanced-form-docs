---
description: >-
  A provider component that propagates the application-wide form settings to all
  children forms.
---

# FormProvider

## Specification

Think of it as of a `Provider` from Redux, only for the forms. This way the forms in your application, regardless of the depth they are rendered in, inherit the options passed to the `<FormProvider>` component.

## Props

| Prop name | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `rules` | [`[ValidationRules: Object]`](../validation/rules.md) | `null` | Validation rules declaration. |
| `messages` | [`[ValidationMessages: Object]`](../validation/messages.md) | `null` | Validation messages declaration. |
| `withImmutable` | `boolean` | `false` | When `true`, all argument properties \(i.e. `fieldProps`, `fields`\) are going to be instances of Immutable. Always provide this property if you are familiar and using Immutable in your project. |
| `debounceTime` | `number` | `250` | Custom debounce duration \(ms\) for onChange field validation. |

## Example

### Rules and messages

Render the `<FormProvider>` on the root-level of your application \(alongside the other providers you may have\):

```jsx
import React from 'react'
import { FormProvider } from 'react-advanced-form'

const App = ({ children }) => (
  <FormProvider rules={ validationRules } messages={ validationMessages }>
    { children }
  </FormProvider>
)
```

### Immutable argument properties

React Advanced Form requires ImmutableJS, as it stores field records using immutable data instances. By providing `withImmutable` prop to the form provider allows you to use those immutable instances without preceding conversion to plain JavaScript. That is handy if you already use ImmutableJS in your application, and can potentially increase the library's performance by skipping unnecessary conversion step.

{% code-tabs %}
{% code-tabs-item title="app/index.js" %}
```jsx
import React from 'react'
import { FormProvider } from 'react-advanced-form'
import Root from './Root'

const App = () => (
    <FormProvider withImmutable>
        <Root />
    </FormProvider>
)

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="app/Root.jsx" %}
```jsx
import React from 'react'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  /* Exposed arguments are immutable instances */
  handleUsernameChange = ({ fieldProps, fields }) => {
    fieldProps.get('value')
    fields.getIn(['fieldGroup', 'anotherField'])
  }

  render() {
    return (
      <Form>
        <Input
          name="username"
          onChange={ this.handleUsernameChange } />
      </Form>
    )
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

