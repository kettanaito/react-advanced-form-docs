# Getting started

The biggest difference when switching to React Advanced Form validation is that it diverges from a conventional single `validate` function and uses a dedicated [validation schema](schema/) to determine the next validity state of the fields.

## Validation types

Any field supports synchronous and asynchronous validation, and any combination of those.

{% hint style="success" %}
React Advanced Form comes with a smart multi-layer validation built-in. Learn more on the [Priority & Exclusion](schema/#priority-and-exclusion) of the validation rules.
{% endhint %}

## Validation schema

The majority of validation rules reside in the dedicated validation schema. It is a good place to start declaring validation in your application.

{% page-ref page="schema/" %}

## Applying validation

There are multiple ways to apply validation to a field \(listed by priority, from highest to lowest\):

* [Field-specific](../components/field/props/rule.md) rules
* [Form-specific](../components/form/props/rules.md) rules
* [Application-wide](../components/form-provider.md) rules

## Validation messages

Validation is a communication between your system and a user. Converse clearly with our versatile API and smart fallback system. Take advantage of the key features of a validation message:

* Completely decoupled from the validation schema
* Each message can be a function that accepts the field's `value`, `fieldProps`, `fields` and `form`, and returns the message string
* Allows to associate a message with a specific rule name

{% page-ref page="messages.md" %}

## Validity state

The result of a validation is reflected in the validity state. It contains two properties:

* `valid` \(boolean\)
* `invalid` \(boolean\)

Those properties can be accessed on the `fieldProps` in a field component declaration and various callback methods. We recommend to base the validation UI based on the validity state.

{% hint style="warning" %}
Please note that `valid` and `invalid` states are not interchangeable, thus:
{% endhint %}

```javascript
!fieldProps.valid !== fieldProps.invalid
```

This value separation is crucial for initial validity state. When a field is mounted, it is neither valid, nor invalid, thus the values of both properties are set to `false`. Further field interactions update the validity state correspondingly.

{% page-ref page="../hoc/create-field/exposed-props.md" %}

## Backwards compatible

We are using a specific validation format—[validation schema](schema/). It is, however, a plain Object that can be used even without React Advanced Form.

