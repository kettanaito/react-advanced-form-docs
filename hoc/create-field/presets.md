# Field presets

Presets contain pre-defined `createField` [options](options.md) relevant to the respective field type. Those options ensure proper field behavior as well as automatically map essential form element's props \(i.e. `placeholder`, `multiselect`, etc.\) from the wrapped component to the actual form element.

Presets are designed for seamless integration of common field types. For the custom fields you may want to consider writing your own presets or extending the existing ones.

## Presets list

There are field presets for all common field types. Those should provide a sensible defaults, therefore it is recommended to use them when declaring a respective field component.

* `fieldPresets.input`
* `fieldPresets.textarea`
* `fieldPresets.checkbox`
* `fieldPresets.select`
* `fieldPresets.radio`

## Example

### Basic

```jsx
import React from 'react'
import { createField, fieldPresets } from 'react-advanced-form'

const Select = ({ children, fieldProps }) => (
  <select {...fieldProps}>
    {children}
  </select>
)

export default createField(fieldPresets.select)(Select)
```

### Extending a preset

```javascript
import React from 'react'
import { createField, fieldPresets } from 'react-advanced-form'

const DateSelect = ({ children, fieldProps }) => (
  <select {...fieldProps}>
    {children}
  </select>
)

export default createField({
  ...fieldPresets.select,
  valuePropName: 'selectedDate',
})(DateSelect)
```

