# Options

## Introduction

Passing options to the `createField()` high-order component allows to control the behavior of the created field. That is extremely useful when implementing custom field logic, or integrating third-party solutions to work with React Advanced Form.

{% hint style="info" %}
You **don't have** to configure any of these options. There are sensible defaults exposed with [Field presets](presets.md), which you can provide as the argument to `createField()`.
{% endhint %}

## `valuePropName`

| Type | `string` |
| :--- | :--- |
| Default value | `"value"` |

Some fields update a prop different from the `value` upon the interaction with them. For example, a checkbox updates its `checked` prop. Provide the prop name to update on field's `onChange` using this option, in case it differs from `value`.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class Checkbox extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<input {...fieldProps} />)
  }
}

export default createField({
  valuePropName: 'checked'
})(Checkbox)
```

## `initialValue`

| Type | `any` |
| :--- | :--- |
| Default value | `''` |

Specifies the initial value of all field instances.

Useful for the cases when the initial value of the field is different from an empty string. For example, when creating a Datepicker you may want to specify the today's date as the initial value for all datepickers.

## `mapValue`

| Type | `any` |
| :--- | :--- |
| Default value | `(value) => value` |

A transformer function to map a field's value on essential value updates.

```jsx
import { createField } from 'react-advanced-form'

export default createField({
  mapValue: (value) => {
    return dateFns.parse(value)
  },
})
```

{% hint style="info" %}
This affects indirect value updates \(i.e. receiving next "value" prop, resetting or clearing a field\). This has no effect when native "onChange" is dispatched.
{% endhint %}

## `allowMultiple`

| Type | `boolean` |
| :--- | :--- |
| Default value | `false` |

Allows multiple instances of the field with the same name within a single form's scope. This affects both form and [Field group](../../components/field-group.md) scopes.

By default, field's `name` serves as the unique identifier, preventing the registration of duplicate fields. However, some field types \(i.e. radio button\) should allow multiple field instances with the same name.

## `mapPropsToField`

### **Definition**

| Type | `(params) => Object` |
| :--- | :--- |
| Default value | `({ fieldRecord }) => fieldRecord` |

### **Parameters**

| Param name | Type | Description |
| :--- | :--- | :--- |
| `valuePropName` | `string` |  |
| `props` | `Object` |  |
| `fieldRecord` | `Object` |  |
| `context` | `Object` |  |

Each field has its record stored in the internal state of the `Form` component. That record is composed based on the field's props, but may \(and sometimes must\) be altered to provide proper field functionality.

To change the initial values of the field record pass this option to the `createField` as follows:

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class Checkbox extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<input {...fieldProps} />)
  }
}

export default createField({
  valuePropName: 'checked',
  mapPropsToField: ({ fieldRecord }) => ({
    ...fieldRecord,
    type: 'checkbox',
    initialValue: props.checked
  })
})(Checkbox)
```

## `enforceProps`

### **Definition**

| Type | `(params) => Object` |
| :--- | :--- |
| Default value | `() => ({})` |

### **Parameters**

| Param name | Type | Description |
| :--- | :--- | :--- |
| `props` | `string` |  |
| `contextProps` | `Object` |  |

This option allows to provide an Object of props which will override the Field's registration record within the form.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class Checkbox extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<input {...fieldProps} />)
  }
}

export default createField({
  valuePropName: 'checked',
  enforceProps: ({ contextProps }) => ({
    checked: contextProps.checked
  })
})(Checkbox)
```

## `beforeRegister`

### **Definition**

| Type | `(params) => Object` |
| :--- | :--- |
| Default value | `({ fieldProps }) => fieldProps` |

### **Parameters**

| Param name | Type | Description |
| :--- | :--- | :--- |
| `fieldProps` | `string` |  |
| `fields` | `Object` |  |

Applies additional transformation or logic to the field right before it is registered. Allows to completely prevent field registration when `false` is returned from this method.

## `shouldValidateOnMount`

### Definition

| Type | `(params) => boolean` |
| :--- | :--- |
| Default value | `() => false` |

### Parameters

| Param name | Type | Description |
| :--- | :--- | :--- |
| `valuePropName` | `any` |  |
| `value` | `any` |  |
| `fieldRecord` | `string` |  |
| `context` | `Object` |  |

Determines whether a field should be validated upon mount.

## `serialize`

### Definition

| Type | `(params) => any` |
| :--- | :--- |
| Default value | `(value) => value` |

### Parameters

| Param name | Type | Description |
| :--- | :--- | :--- |
| `value` | `any` | Original serialized value of a field. |

A custom serialization transformer function applied during the field's serialization.

```jsx
export default createField({
  serialize(value) {
    return dateFns.format(value, 'MM/DD/YYYY')
  },
})
```

{% hint style="info" %}
Note that `serialize` works **complementary** with [`Form.props.onSerialize`](../../components/form/callbacks/onserialize.md), and it executed before the form-wide serialization transformer.
{% endhint %}

