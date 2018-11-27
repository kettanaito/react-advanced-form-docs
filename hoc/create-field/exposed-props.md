# Exposed props

Wrapping a React component in `createField` high-order component automatically exposes the properties listed below. These properties can be used for field styling and custom logic or behavior.

## Props list

| Prop name | Type | Description |
| :--- | :--- | :--- |
| `fieldProps` | `Object` | Object of essential props for the primitive field components \(i.e. input, select, textarea, etc\). |
| `fieldState` | `Object` | Object representing a field's state. |

> `fieldProps` are composed from the `fieldState` and are exposed separately to ease the process of props assignment to the form elements.

## `fieldState`

Object representing a field's state.

### General

| Prop name | Type | Description |
| :--- | :--- | :--- |
| `required` | `boolean` | Indicates whether the field is required. |
| `disabled` | `boolean` | Indicates whether the field is disabled. |
| `skip` | `boolean` | Indicates whether the field should be skipped during any serialization process. Read more about [`Field.props.skip`](../../components/field/props/skip.md). |

### Validity state

| Prop name | Type | Description |
| :--- | :--- | :--- |
| `valid` | `boolean` | Indicates whether the field has passed all the validations. |
| `invalid` | `boolean` | Indicates whether the field has not passed all the validations. |

### Validation

| Prop name | Type | Description |
| :--- | :--- | :--- |
| `validating` | `boolean` | Indicates whether the field is being validated at the moment. |
| `errors` | `string[]` | Collection of the validation errors relative to the fields at the given point of time. |
| `validated` | `boolean` | Indicates that the field has been validated, regardless of the validation type and status. |
| `validatedSync` | `boolean` | Indicates whether the field has been validated synchronously. |
| `validSync` | `boolean` | Indicates whether the field is valid relatively to its synchronous validation rules. |
| `validatedAsync` | `boolean` | Indicates whether the field has been validated asynchronously. |
| `validAsync` | `boolean` | Indicates whether the field is valid relatively to its asynchronous validation rules. |

## Example

Exposed props can be accessed in `this.props` of your component.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class CustomField extends React.Component {
  render() {
    const { fieldProps, fieldState } = this.props
    const { valid, invalid, errors } = fieldState

    return (<input {...fieldProps} />)
  }
}

export default createField()(CustomField)
```

