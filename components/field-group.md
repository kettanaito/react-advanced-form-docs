# Field.Group

## Specification

A component responsible for form data separation on the layout level. Designed primarily for handling of complex forms and semantic representation of fields structure expected by a remote end-point.

{% hint style="info" %}
Beware that grouping the fields affects how you reference them in the serialized object, or reactive resolvers.
{% endhint %}

## Props

| Prop name | Type | Description |
| :--- | :--- | :--- |
| `name` | `string` | The name of the field group. All the fields wrapped in `Field.Group` will be available by the following reference path: `[...groupNames, fieldName]`. |

## Example

### Basic

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        <Field.Group name="primaryInfo">
          <Input
            name="username"
            value="admin" />
          <Input
            name="firstName"
            value="John" />
        </Field.Group>

        <Input name="city" value="London" />
      </Form>
    );
  }
}
```

The form above serializes into the following JSON:

```javascript
{
  "city": 'London',
  "primaryInfo": {
    "username": 'admin',
    "firstName": 'John'
  }
}
```

> **Tip:** `Field.Group` allows you to have multiple fields with _the same name_ under one Form, as long as there are no same names within one group \(root, or custom field groups\).

### Nested groups

It is possible to nest field groups. Nested field groups name paths are going to be merged the same way as the [Split groups](field-group.md#split-groups). That allows to nest and split groups at the same time.

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Inpu } from 'react-advanced-form-addons'

export default class NestedGroups extends React.Component {
  render() {
    return (
      <Form>
        <Field.Group name="primaryInfo">
          <Input
            name="email"
            type="email"
            value="john@maverick.com" />

          <Field.Group name="billingAddress">
            <Input
              name="firstName"
              value="John" />
            <Input
              name="lastName"
              value="Maverick" />
          </Field.Group>
        </Field.Group>
      </Form>
    )
  }
}
```

Will be serialized into the following JSON:

```javascript
{
  "primaryInfo": {
    "email": "john@maverick.com",
    "billingAddress": {
      "firstName": "John",
      "lastName": "Maverick"
    }
  }
}
```

### Split groups

One of the benefits of `Field.Group` is an ability to have multiple groups with the same name, which will group the elements under one property upon the serialization. This is particularly useful when UI was not, or cannot be designed according to the data structure expected by the remote end-point.

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        <Input
          name="email"
          value="admin@site.com" />

        <h3>Billing address</h3>
        <Field.Group name="billingAddress">
          <Input
            name="firstName"
            value="John" />
          <Input
            name="lastName"
            value="Maverick" />
        </Field.Group>

        <h3>Delivery address</h3>
        <Field.Group name="billingAddress">
          <Input
            name="firstName"
            value="Kate" />
          <Input
            name="lastName"
            value="Rosewood" />
        </Field.Group>

        <h3>Contact details</h3>
        <Field.Group name="billingAddress">
          <Input
            name="phoneNumber"
            value="123456789" />
        </Field.Group>
        <Field.Group name="deliverAddress">
          <Input
            name="address"
            value="Baker st." />
        </Field.Group>
      </Form>
    )
  }
}
```

The layout above will serialize into the following JSON:

```javascript
{
    "email": "admin@site.com",
    "billingAddress": {
        "firstName": "John",
        "lastName": "Maverick",
        "phoneNumber": "123456789"
    },
    "deliveryAddress": {
        "firstName": "Kate",
        "lastName": "Rosewood",
        "address": "Baker st."
    }
}
```



