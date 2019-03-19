# Options

## Introduction

Passing options to the `createField()` high-order component allows to control the behavior of the created field. That is extremely useful when implementing custom fields, or integrating third-party solutions to work with React Advanced Form.

{% hint style="info" %}
You **don't have** to configure any of these options. Please use the defaults exposed with [Field presets](presets.md), unless you're customizing a field's behavior on purpose.
{% endhint %}

## `valuePropName`

| Type | `string` |
| :--- | :--- |
| Default value | `"value"` |

Some fields update a prop different from the `value` upon the interaction with them. For example, a checkbox updates its `checked` prop. Provide the prop name to update on field's `onChange` using this option, in case it differs from `value`.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

const Checkbox = (props) => {
  const { fieldProps } = props
  return (<input {...fieldProps} />)
}

export default createField({
  valuePropName: 'checked',
})(Checkbox)
```

## `initialValue`

| Type | `any` |
| :--- | :--- |
| Default value | `''` |

Initial value of all instances of a field. Useful for cases when the initial value of a field is different from an empty string.

```jsx
export default createField({
  /**
   * Set initial value to the current date
   * instead of an empty string (default).
   */
  initialValue: Date.now(),
})(Datepicker)
```

{% hint style="info" %}
Note that `initialValue` is then mapped using `mapValue` option.
{% endhint %}

## `assertValue`

| Type | `(params) => boolean` |
| :--- | :--- |
| Default value | `({ value }) => !!value` |

A predicate function stating that a field contains some value.

Useful for describing a proper validation behavior for a custom field where its value is represented using a complex instance \(i.e. Object\).

```jsx
export default createField({
  valuePropName: 'range',
  mapValue: (value) => ({
    from: value[0],
    to: value[1],
  }),
  assertValue: (range) => {
    return range.from || range.to
  },
})(RangeInput)
```

In the example above, we have created a field that accepts an array of integers as its `value`, and transforms it into the `{ from, to }` Object to be stored in the field's state. In order to have a proper validation logic, such as validation on mount, we need to supply a custom predicate that describes when our field has some actual value. 

## `mapValue`

| Type | `any` |
| :--- | :--- |
| Default value | `(value) => value` |

Maps a "raw" field's value into its representative in the field's state.

```jsx
import { createField } from 'react-advanced-form'

export default createField({
  mapValue: (value) => {
    return dateFns.parse(value)
  },
})(Datepicker)
```

{% hint style="info" %}
This only affects external value updates \(i.e. receiving next `value` prop, resetting or clearing a field\). This has no effect when the native `onChange` callback is dispatched.
{% endhint %}

## `allowMultiple`

| Type | `boolean` |
| :--- | :--- |
| Default value | `false` |

Allows multiple instances of a field with the same name within a single form's scope. This affects both form and [Field group](../../components/field-group.md) scopes.

By default, field's name is the unique identifier that prevents the registration of duplicate fields. However, some field types \(i.e. radio button, or your custom field\) may want to render multiple field components with the same name.

## `mapPropsToField`

### **Definition**

| Type | `(params) => Object` |
| :--- | :--- |
| Default value | `({ fieldRecord }) => fieldRecord` |

### **Parameters**

| Param name | Type | Description |
| :--- | :--- | :--- |
| `valuePropName` | `string` | Value prop name of a field. |
| `props` | `Object` | Raw field component's props. |
| `fieldRecord` | `Object` | Reference to the field's record in the form's state. |
| `context` | `Object` |  |

Each field has its record stored in the internal state of the `Form` component. That record is composed based on the field's props, but may \(and sometimes must\) be altered to provide proper field functionality.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

const Checkbox = (props) => {
  const { fieldProps } = props
  return (<input {...fieldProps} />)
}

export default createField({
  valuePropName: 'checked',
  mapPropsToField: ({ fieldRecord }) => ({
    ...fieldRecord,
    type: 'checkbox',
    initialValue: props.checked,
  }),
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
| `props` | `string` | Raw field component's props. |
| `contextProps` | `Object` | Field record in a form's state. |

Allows enforcing an Object of props which will override the Field's registration record within the form.

```jsx
import React from 'react'
import { createField } from 'react-advanced-form'

const Checkbox = (props) => {
  const { fieldProps } = props
  return (<input {...fieldProps} />)
}

export default createField({
  valuePropName: 'checked',
  enforceProps: ({ contextProps }) => ({
    checked: contextProps.checked,
  }),
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
| `fieldProps` | `string` | Original field props. |
| `fields` | `Object` | Reference to all fields. |

Applies additional transformation or logic to the field right before it is registered. Allows to completely prevent field registration when `false` is returned from this method.

#### Modifying field's record

```jsx
export default createField({
  beforeRegister: ({ fieldProps, fields }) => {
    return {
      ...fieldProps,
      /**
       * Add a custom property "customProp"
       * on the field's record in the state.
       */
      customProp: 'foo',
    }
  }
})(FieldComponent)
```

#### Preventing field registration

Returns `false` from `beforeRegister` method to prevent a field from registering its record in the parent form's state.

```jsx
export default createField({
  beforeRegister: ({ fieldProps, fields }) => {
    const inputProps = fieldProps.getRef().props
    
    /* Prevent field registration if it has "foo" prop */
    if (inputProps.hasOwnProperty('foo')) {
      return null
    }
    
    return fieldProps
  }
})(FieldComponent)
```

## `shouldValidateOnMount`

### Definition

| Type | `(params) => boolean` |
| :--- | :--- |
| Default value | [`assertValue`](options.md#assertvalue) |

Determines whether a field should be validated upon mounting, if it has value \(its `assertValue` resolves\).

### Parameters

| Param name | Type | Description |
| :--- | :--- | :--- |
| `[valuePropName]` | `any` | Dynamic key that is value prop name, with value being a field's value. |
| `valuePropName` | `string` | Value prop name of a field. |
| `fieldRecord` | `string` | Reference to a field's record in a form's state. |
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

Returns the next serialization payload of a field.

Useful to provide transformations to a field's value upon form serialization.

```jsx
export default createField({
  /**
   * Let's say we have a Datepicker component that
   * stores his value as a DateFNS instance. We can
   * format its value into a date string when
   * the field is serialized.
   */
  serialize(value) {
    return dateFns.format(value, 'MM/DD/YYYY')
  },
})(Datepicker)
```

{% hint style="info" %}
Note that `serialize` works **complementary** with [`Form.props.onSerialize`](../../components/form/callbacks/onserialize.md), and it executed _before_ the form's serialization transformer.
{% endhint %}

