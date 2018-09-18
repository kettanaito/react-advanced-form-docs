# FormProvider

## Specification

A provider component that propagates application-wide form settings to all children forms.

## Props

| Prop name | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| `rules` | [ValidationSchema](../validation/schema/) | `undefined` | Validation rules schema. |
| `messages` | [`[ValidationMessages: Object]`](../validation/messages.md) | `unedfined` | Validation messages. |
| `debounceTime` | `number` | `250` | Custom debounce duration \(ms\) for `onChange` field validation. |

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



