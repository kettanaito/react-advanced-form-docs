# Getting started

The biggest difference when switching to React Advanced Form validation is that it diverges from a conventional single `validate` function and uses a dedicated **validation schema** to determine the next validity state of the fields.

## Validation types

Any field supports synchronous and asynchronous validation, and any combination of those.

{% hint style="info" %}
React Advanced Form comes with a smart multi-layer validation logic built-in. Learn more on the [Priority & Exclusion](schema/#priority-and-exclusion) of the validation rules.
{% endhint %}

## Applying validation

There are multiple ways to apply validation to a field \(listed by priority, from highest to lowest\):

* [Field-specific](../components/field/props/rule.md) rules,
* [Form-specific](../components/form/props/rules.md) rules,
* [Application-wide](../components/form-provider.md) rules.

## Validation schema

{% hint style="info" %}
Heart and soul of validation is the [Validation schema](schema/).
{% endhint %}

## Validation messages

> Explain how validation messages work. Highlight similarity in definition to validation rules.

## === Messages

Validation messages always follow the corresponding rules. In React Advanced Form those two are completely separated, allowing you to have multi-lingual validation messages while using the same validation rules.

### Features

* **Flexibility.** Utilize any known data to compose a proper message: use `value`, `fieldProps`, `fields` and even `form` references to craft the validation message you need.
* **Precision.** Return specific message for specific rule natively, forget about those work-arounds.
* **Fallback messages.** A reach fallback algorithm grants you a precise control over which messages is being displayed at the moment. Missing a message for the rejected validation rule? We have got you covered!

Read more on [Validation messages](messages.md).

