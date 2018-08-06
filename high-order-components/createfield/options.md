# Options

> This topic is related to [`createField`](https://github.com/kettanaito/react-advanced-form/tree/75c444924d87ca8ff76bc096231173e42e717adc/docs/hoc/createField/basics.md) high-order component. Make sure to understand the context it is being described in.

## Introduction

Passing options to the `createField()` high-order component allows to control the behavior of the created field. That is extremely useful when implementing the fields with custom logic, or integrating third-party solutions to work with React Advanced Form.

{% hint style="info" %}
You **don't have** to configure any of these options. There are sensible defaults exposed with [Field presets](presets.md), which you can provide as an argument to `createField()`.
{% endhint %}

## Options list

| Option name | Type | Description |
| :--- | :--- | :--- |
| `valuePropName` | `string` | A custom prop name to be treated as an updatable value during the field value change. |
| `initialValue` | `any` | Custom initial value applied to all field instances by default. |
| `allowMultiple` | `boolean` | Dictates whether multiple instances of the field with the same name is allowed. |
| `mapPropsToField` | `({ props, context, fieldRecord, valuePropName }) => Object` | A custom maping function which should return a props Object used as the initial props during the field registration. |
| `enforceProps` | `({ props, contextProps }) => Object` | A function which should return a props Object to be enforced on the custom field. |
| `beforeRegister` | `({ fieldProps, fields }) => fieldProps` | Applies additional transformations to the `fieldProps`, or prevents from fields registration when returns `false`. |
| `shouldValidateOnMount` | `({ props, fieldRecord, valuePropName, context }) => boolean` | Controls the necessity of validation upon field mount. |

## `valuePropName: string`

**Default value:** `value`

Some fields update a prop different from the `value` upon the interaction with them. For example, a checkbox updates its `checked` prop. Provide the prop name to update on field's `onChange` using this option, in case it differs from `value`.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class Checkbox extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<input { ...fieldProps } />)
  }
}

export default createField({
  valuePropName: 'checked'
})(Checkbox)
```

## `initialValue: any`

**Default value:** `''`

Allows to specify the initial value for all field instances.

Useful for the cases when the initial value of the field is different from an empty string. For example, when creating a Datepicker you may want to specify the today's date as the initial value for all datepickers.

## `allowMultiple: boolean`

**Default value:** `false`

Allows multiple instances of the field with the same name under a single form scope.

By default, field's `name` serves as the unique identifier, preventing the registration of duplicate fields. However, some field types \(i.e. radio button\) should allow multiple field instances with the same name.

## `mapPropsToField: ({ props, context, fieldRecord, valuePropName }) => Object`

**Default value:** `({ fieldRecord }) => fieldRecord`

Each field has its record stored in the internal state of the `Form` component. That record is composed based on the field's props, but may \(and sometimes must\) be altered to provide proper field functionality.

To change the initial values of the field record pass this option to the `createField` as follows:

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class Checkbox extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<input { ...fieldProps } />)
  }
}

export default createField({
  valuePropName: 'checked',
  mapPropsToField: ({ props, fieldRecord, valuePropName }) => ({
    ...props,
    type: 'checkbox',
    initialValue: props.checked
  })
})(Checkbox)
```

## `enforceProps: ({ props, contextProps }) => Object`

**Default value:** `() => ({})`

This option allows to provide an Object of props which will override the Field's registration record within the form.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

class Checkbox extends React.Component {
  render() {
    const { fieldProps } = this.props

    return (<input { ...fieldProps } />)
  }
}

export default createField({
  valuePropName: 'checked',
  enforceProps: ({ props, contextProps }) => ({
    checked: contextProps.get('checked')
  })
})(Checkbox)
```

> Note that `contextProps` is an instance of [Immutable Map](https://facebook.github.io/immutable-js/docs/#/Map).

## `beforeRegister: ({ fieldProps, fields }) => fieldProps`

**Default value:**

```javascript
{
  beforeRegister({ fieldProps, fields }) {
    return fieldProps
  }
}
```

Applies additional transformation or logic to the field right before it is registered. Allows to completely prevent field registration when `false` is returned from this method.

## `shouldValidateOnMount: ({ props, fieldRecord, valuePropName, context }) => boolean`

**Default value:**

```javascript
{
  shouldValidateOnMount({ fieldRecord, valuePropName }) {
    const fieldValue = fieldRecord[valuePropName]
    return isset(fieldValue) && (fieldValue !== '')
  }
}
```

Determines whether to validate the field upon mount.

