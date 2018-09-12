# Table of contents

* [Introduction](README.md)

## General

* [Introduction](general/introduction.md)
* [FAQ](general/faq.md)
* [Migration guides](general/migration/README.md)
  * [1.4.x → 1.5.x](general/migration/1.4.x-1.5.x.md)

## Getting started

* [Installation](getting-started/installation.md)
* [Creating fields](getting-started/creating-fields.md)
* [Creating form](getting-started/creating-form.md)
* [Validation rules](getting-started/validation-rules.md)
* [Validation messages](getting-started/validation-messages.md)
* [Applying validation](getting-started/applying-validation.md)
* [Handle submit](getting-started/handle-submit.md)

## Architecture

* [Argument properties](architecture/argument-properties.md)
* [Referencing](architecture/referencing.md)
* [Field lifecycle](architecture/field-lifecycle.md)
* [Reactive props](architecture/reactive-props.md)

## High-order components

* [createField](high-order-components/createfield/README.md)
  * [Options](high-order-components/createfield/options.md)
  * [Field presets](high-order-components/createfield/presets.md)
  * [Exposed props](high-order-components/createfield/exposed-props.md)

## Components

* [FormProvider](components/formprovider.md)
* [Form](components/form/README.md)
  * [Props](components/form/props/README.md)
    * [innerRef](components/form/props/innerref.md)
    * [initialValues](components/form/props/initialvalues.md)
    * [action](components/form/props/action.md)
    * [rules](components/form/props/rules.md)
    * [messages](components/form/props/messages.md)
  * [Methods](components/form/methods/README.md)
    * [setErrors\(\)](components/form/methods/seterrors.md)
    * [reset\(\)](components/form/methods/reset.md)
    * [validate\(\)](components/form/methods/validate.md)
    * [serialize\(\)](components/form/methods/serialize.md)
    * [submit\(\)](components/form/methods/submit.md)
  * [Callbacks](components/form/callbacks/README.md)
    * [onFirstChange](components/form/callbacks/onfirstchange.md)
    * [onReset](components/form/callbacks/onreset.md)
    * [onInvalid](components/form/callbacks/oninvalid.md)
    * [onSerialize](components/form/callbacks/onserialize.md)
    * [onSubmitStart](components/form/callbacks/onsubmitstart.md)
    * [onSubmitted](components/form/callbacks/onsubmitted.md)
    * [onSubmitFailed](components/form/callbacks/onsubmitfailed.md)
    * [onSubmitEnd](components/form/callbacks/onsubmitend.md)
* [Field.Group](components/field.group.md)
* [Field](components/field/README.md)
  * [Props](components/field/props/README.md)
    * [rule](components/field/props/rule.md)
    * [asyncRule](components/field/props/asyncrule.md)
    * [skip](components/field/props/skip.md)
  * [Callbacks](components/field/callbacks/README.md)
    * [onFocus](components/field/callbacks/onfocus.md)
    * [onChange](components/field/callbacks/onchange.md)
    * [onBlur](components/field/callbacks/onblur.md)

## Validation

* [Getting started](validation/getting-started.md)
* [Behavior](validation/behavior.md)
* [Validation schema](validation/schema/README.md)
  * [Rule definition](validation/schema/rule-definition.md)
  * [Reactive rules](validation/schema/reactive-rules.md)
* [Logic](validation/logic.md)
* [Rules](validation/rules.md)
* [Messages](validation/messages.md)

## Developers

* [Contributing](developers/contributing.md)
* [Testing](developers/testing.md)

## Recipes

* [Utilizing functions](recepies/reducing-boilerplate.md)

