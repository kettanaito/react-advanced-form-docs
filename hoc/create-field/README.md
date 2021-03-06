# createField

## Specification

A high-order component which enhances the provided custom component \(`WrappedComponent`\) to behave as React Advanced Form field. When being wrapped, all component interactions are handled by the parent `Form` automatically, exposing the internal field props and field state to the wrapped component.

`createField` is designed for both field styling and  custom fields implementation.

> It is important to understand the [Field lifecycle](../../architecture/field-lifecycle.md) before creating custom fields. This will significantly reduce the amount of questions and increase the developer's experience.

## Example

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class CustomField extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<MyComponent {...fieldProps} />)
  }
}

export default createField({...})(CustomField)
```

> It's crucial to propagate the `CustomComponent.props.fieldProps` to `MyComponent` for it to have the essential props and event handlers of the native field.

