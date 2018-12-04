# Introduction

[![Package version](https://img.shields.io/npm/v/react-advanced-form.svg)](https://www.npmjs.com/package/react-advanced-form) [![Build status](https://img.shields.io/circleci/project/github/kettanaito/react-advanced-form/master.svg)](https://circleci.com/gh/kettanaito/react-advanced-form) [![Vulnerabilities](https://snyk.io/test/github/kettanaito/react-advanced-form/badge.svg)](https://snyk.io/test/github/kettanaito/react-advanced-form) [![Dependencies status](https://img.shields.io/david/kettanaito/react-advanced-form.svg)](https://david-dm.org/kettanaito/react-advanced-form) [![DevDepenencies status](https://img.shields.io/david/dev/kettanaito/react-advanced-form.svg)](https://david-dm.org/kettanaito/react-advanced-form?type=dev) 

![](.gitbook/assets/logo.png)

[React Advanced Form](https://github.com/kettanaito/react-advanced-form) is a library for tailoring real-world forms in [React](https://reactjs.org/) with pleasure and ease.

## Features

### Expectations shift

Our primary goal is to educate developers to trust and expect a form to do more than just rendering the fields. Our features are designed to handle cumbersome use cases with clean and performant code.

### Immutable

Each field interaction or update is a function that produces the next state of a field.

### Composite fields

React Advanced Form is **field-centric**. That means that you define field components and reuse them throughout the entire application. Utilize reach field API to reflect even the most granular field state changes in the user interface.

{% page-ref page="getting-started/creating-fields.md" %}

### **Fast and clean**

Form declaration must be simple, easy to read and maintain.

```jsx
// No, this is not a diminished example, this is a completely working form
<Form action={this.registerUser}>
  <Input name="username" required />
  <Input name="password" type="password" required />
</Form>
```

{% page-ref page="getting-started/creating-form.md" %}

### Layered validation

Select the field\(s\) based on type or name, and declare validation resolver functions.

```javascript
export default {
  type: {
    password: {
      capitalLetter: ({ value }) => /[A-Z]/.test(value),
      oneNumber: ({ value }) => /[0-9]/.test(value),
    },
  },
  name: {
    confirmPassword: ({ get, value }) => {
      /**
       * The "confirmPassword" field will be re-validated
       * whenever the "value" prop of "userPassword" field updates.
       */
      return value === get(["userPassword", "value"])
    },
  },
};
```

Access the field's `value`, `fieldProps` and the `form` as the parameters of each resolver function. **Say goodbye to crowded** `validate` **functions, welcome clean validation schemas**!

{% page-ref page="validation/getting-started.md" %}

### Reactive props

How much effort would it take you to make one field required based on another field\(s\)? Yes, the correct answer is—_one line of code_:

```jsx
<Input
  name="firstName"
  required={({ get }) => !!get(['lastName', 'value'])} />
<Input
  name="lastName"
  required={({ get }) => !!get(['firstName', 'value'])} />
```

Get as many data from the sibling fields as needed, and build your logic on that. Embrace the power of reactive programming, which re-evaluates a resolver function whenever the referenced field props update.

{% page-ref page="architecture/reactive-props.md" %}

### Field grouping

Designed to tackle API misalignment, field grouping allows to control the serialized data structure of a form on the layout level. Take advantage of nested, split or exact groups.

```jsx
<Input name="companyName" value="Google" />

<Field.Group name="billingAddress">
  <Input name="firstName" value="John" />
  <Input name="lastName" value="Maverick" />
</Field.Group>

<Checkbox name="termsAndConditions" checked />

<Field.Group name="deliveryAddress">
  <Input name="firstName" value="Catheline" />
  <Input name="lastName" value="McCoy" />
</Field.Group>
```

The form above serializes into the following JSON:

```javascript
{
  "companyName": "Google",
  "billingAddress": {
    "firstName": "John",
    "lastName": "Maverick"
  },
  "termsAndConditions": true,
  "deliveryAddress": {
    "firstName": "Catheline",
    "lastName": "McCoy"
  }
}
```

{% page-ref page="components/field-group.md" %}

### **Third-party integration**

Turn any component \(including a third-party one\) into a field, which validates, serializes, and behaves just as any other field. Alternatively, you can build a field with the entirely custom logic.

{% page-ref page="hoc/create-field/" %}

## Getting started

### Install

```bash
npm install react-advanced-form --save
```

> Make sure to have [React](https://github.com/facebook/react) \(15.0+\) installed in your project.

### Guidelines

Starting with something new may appear challenging. There is a step-by-step instructions on how to get started with React Advanced Form, which ensure easy and clear integration process.

{% page-ref page="getting-started/installation.md" %}

## Resources

* [**Documentation**](https://kettanaito.gitbooks.io/react-advanced-form)\*\*\*\*
* "[Advanced forms in React made easy](https://medium.com/@kettanaito/advanced-forms-in-react-made-easy-92a6e208f017)" — Artem Zakharchenko \(Medium\)

## Browser support

| Chrome | Firefox | Safari | iOS Safari | Edge | Internet Explorer |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 65+ | 57+ | 9+ | 8+ | 41+ | – |

> **There is no official support for Internet Explorer**. There is no testing conducted for that browser. Consider educating the web and deprecating support for obsolete browsers.

## Live examples

* [Synchronous validation](https://codesandbox.io/s/53wlvmp42l?module=%2Fsrc%2FSyncValidation.js)
* [Asynchronous validation](https://codesandbox.io/s/73236qlk06?module=%2Fsrc%2FAsyncValidation.js)

## Contributing

Any of your contributions are highly appreciated! See the [Contribution guidelines](https://kettanaito.gitbooks.io/react-advanced-form/docs/CONTRIBUTING.html) to get to know the process better. Moreover, development isn't the only way to contribute, there are [many more](https://kettanaito.gitbooks.io/react-advanced-form/docs/CONTRIBUTING.html#other-contributions).

