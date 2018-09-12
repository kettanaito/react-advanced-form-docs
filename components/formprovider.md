# FormProvider

## Specification

A provider component that propagates application-wide form settings to all children forms.

Primarily designed to distribute consistent validation rules and messages throughout the forms in your application.

## Props

| Prop name | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `rules` | [`[ValidationRules: Object]`](../validation/rules.md) | `null` | Validation rules schema. |
| `messages` | [`[ValidationMessages: Object]`](../validation/messages.md) | `null` | Validation messages. |
| `debounceTime` | `number` | `250` | Custom debounce duration \(ms\) for onChange field validation. |

## Example

Render the `<FormProvider>` on the root-level of your application \(alongside the other providers you may have\):

```jsx
import React from 'react'
import { FormProvider } from 'react-advanced-form'

const App = ({ children }) => (
  <FormProvider rules={validationRules} messages={validationMessages}>
    {children}
  </FormProvider>
)
```



