# Creating fields

> Code examples in this documentation are using field component from the `react-advanced-form-addons` package for the illustrational purposes only. We recommend to define your own set of fields that suit your project's needs foremost.

Integration of React Advanced Form in your application begins from creating a set of reusable fields components. Those are later used to compose any form.

## Implementation

A field is a React component wrapped in the createField high-order component exposed by the library. The wrapper ensures essential field functionality and allows to customize the field's behavior. It also binds internal field's state to reflect in the UI. 

Let's create a simple `Input` field component.

```jsx
import React from 'react'
import { createField, fieldPresets } from 'react-advanced-form'

const Input = (props) => {
  const { fieldProps, fieldState } = props
  const { errors } = fieldState
  
  return (
    <div className="input">
      <input {...fieldProps} />
      
      {/* Render input errors underneath */}
      {errors && errors.map((error) => (
        <div className="text--red">{error}</div>
      ))
    </div>
  )
}

export default createField(fieldPresets.input)(Input)
```

There are a few important things happening in the snippet above:

1. Mapping `fieldProps` to the actual input element.
2. Using `fieldPresets.input` to have essential options for the input element.
3. ...

---

To declare a field you need to create a React component and wrap it in the `createField` high-order component. By doing so, the field can automatically access such information as its validation status, error messages, and much more \(see the full list of [Exposed props](../high-order-components/createfield/exposed-props.md)\).

Fields will often require to use additional [Field presets](../high-order-components/createfield/presets.md) as the argument to the high-order component. Those presets automatically remap essential form elements' props relevant to the field type, and ensure the proper functionality of the fields.

Read the documentation on how to use [`createField`](https://github.com/kettanaito/react-advanced-form/tree/75c444924d87ca8ff76bc096231173e42e717adc/docs/hoc/createField/basics.md), and see the [Examples](creating-fields.md#examples) below for a more practical overview.

## Examples

We recommend looking into the fields components used internally for testing of React Advanced Form. There we used Bootstrap 4 form layout, however, the appearance of your fields is completely up to you.

### Common

* [Input](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Input.jsx)
* [Radio](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Radio.jsx)
* [Checkbox](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Checkbox.jsx)
* [Select](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Select.jsx)
* [Textarea](https://github.com/kettanaito/react-advanced-form/tree/master/examples/fields/Textarea.jsx)

### Third-party

* [react-datepicker](https://github.com/kettanaito/react-advanced-form/blob/master/examples/third-party/react-datepicker/Datepicker.jsx)
* [react-select](https://github.com/kettanaito/react-advanced-form/blob/master/examples/third-party/react-select/Select.jsx)
* [react-lider](https://github.com/kettanaito/react-advanced-form/blob/master/examples/third-party/react-slider/Slider.jsx)

