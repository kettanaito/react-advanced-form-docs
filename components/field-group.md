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

## Basic

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        <Field.Group name="primaryInfo">
          <Input name="username" value="admin" />
          <Input name="firstName" value="John" />
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
  "city": "London",
  "primaryInfo": {
    "username": "admin",
    "firstName": "John"
  }
}
```

> **Tip:** `Field.Group` allows you to have multiple fields with _the same name_ in a single Form, as long as there are no namespace collision within one group.

## Nested groups

Nested `Field.Group` components cascade by their names as their appear in the tree:

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return(
      <Form>
        <Field.Group name="first">
          <Input name="fieldOne" value="foo" />
          <Field.Group name="second">
            <Input name="fieldOne" value="bar" />
          </Field.Group>
        </Field.Group>
      </Form>
    )
  }
}
```

Serializes into the following JSON:

```javascript
{
  "first": {
    "fieldOne": "foo",
    "second": {
      "fieldOne": "bar"
    }
  }
}
```

{% hint style="warning" %}
Escaping of cascading is not currently supported.
{% endhint %}

## Split groups

One of the benefits of `Field.Group` is an ability to have multiple groups with the same name, which will group the elements under one property upon the serialization. This is particularly useful when UI was not, or cannot be designed according to the data structure expected by the remote end-point.

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  render() {
    return (
      <Form>
        <Input name="email" value="admin@site.com" />

        <Field.Group name="billingAddress">
          <Input name="firstName" value="John" />
          <Input name="lastName" value="Maverick" />
        </Field.Group>

        <Field.Group name="billingAddress">
          <Input name="firstName" value="Kate" />
          <Input name="lastName" value="Rosewood" />
        </Field.Group>

        <Field.Group name="billingAddress">
          <Input name="phoneNumber" value="123456789" />
        </Field.Group>
        
        <Field.Group name="deliverAddress">
          <Input name="address" value="Baker st." />
        </Field.Group>
      </Form>
    )
  }
}
```

Serialize into the following JSON:

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



