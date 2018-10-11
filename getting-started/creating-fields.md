# Creating fields

> Code examples in this documentation are using field component from the `react-advanced-form-addons` package for the illustrational purposes only. We recommend to define your own set of fields that suit your project's needs foremost.

Integration of React Advanced Form in your application begins from creating a set of reusable fields components. Those are later used to compose any form.

## Implementation

A field is a React component wrapped in the `createField` high-order component exposed by the library. The wrapper ensures essential field functionality and allows to customize a field's behavior. It also binds internal field's state to reflect in the UI. 

Let's create a simple text input component:

```jsx
import React from 'react'
import { createField, fieldPresets } from 'react-advanced-form'

const Input = (props) => {
  /**
   * "fieldProps" need to be mapped to the field element.
   * "fieldState" contains the current state of a field.
   */
  const { fieldProps, fieldState } = props
  const { errors } = fieldState
  
  return (
    <div className="input">
      {/* Propagating "fieldProps" is crucial to register a field */}
      <input {...fieldProps} />
      
      {/* Render input errors underneath */}
      {errors && errors.map((error) => (
        <div className="text--red">{error}</div>
      ))}
    </div>
  )
}

export default createField(fieldPresets.input)(Input)
```

There are a few important things happening in the snippet above:

1. Mapping `fieldProps` to the actual input element.
2. Using `fieldPresets.input` [preset](../hoc/create-field/presets.md) to have essential options for the input element.
3. Using `fieldState` to reflect field state in the UI.

## Examples

Take a look into the field components used internally for the integration testing of the library.

### Common

* [Input](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Input.jsx)
* [FileInput](https://github.com/kettanaito/react-advanced-form/blob/master/examples/fields/FileInput.jsx)
* [Radio](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Radio.jsx)
* [Checkbox](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Checkbox.jsx)
* [Select](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Select.jsx)
* [Textarea](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Textarea.jsx)

### Third-party

React Advanced Form can be used with any third-party field library.

* [react-datepicker](https://github.com/kettanaito/react-advanced-form/blob/master/examples/third-party/react-datepicker/Datepicker.jsx)
* [react-select](https://github.com/kettanaito/react-advanced-form/blob/master/examples/third-party/react-select/Select.jsx)
* [react-lider](https://github.com/kettanaito/react-advanced-form/blob/master/examples/third-party/react-slider/Slider.jsx)

