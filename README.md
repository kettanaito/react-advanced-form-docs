# Introduction

[![Package version](https://img.shields.io/npm/v/react-advanced-form.svg)](https://www.npmjs.com/package/react-advanced-form) [![Build status](https://img.shields.io/circleci/project/github/kettanaito/react-advanced-form/master.svg)](https://circleci.com/gh/kettanaito/react-advanced-form) [![Vulnerabilities](https://snyk.io/test/github/kettanaito/react-advanced-form/badge.svg)](https://snyk.io/test/github/kettanaito/react-advanced-form) [![Dependencies status](https://img.shields.io/david/kettanaito/react-advanced-form.svg)](https://david-dm.org/kettanaito/react-advanced-form) [![DevDepenencies status](https://img.shields.io/david/dev/kettanaito/react-advanced-form.svg)](https://david-dm.org/kettanaito/react-advanced-form?type=dev) 

![React Advanced Form](.gitbook/assets/logo.png)

## React Advanced Form

[React Advanced Form](https://github.com/kettanaito/react-advanced-form) is a library for tailoring real-world forms in [React](https://reactjs.org/) with pleasure and ease.

No boilerplate. No obscure high-order component configurations. No redundant state management. Embrace powerful custom styling, field grouping, advanced multi-layer validation, validation messages with smart fallback system, reactive props resolvers and much more.

### Features

* **Changing expectations**. Trust and expect a form to do more than just rendering the fields. Our features are designed to handle cumbersome use cases with clean and performant code.
* **Immutable**. Each interaction or update is a pure function that produces the next state of a field.
* [**Composite fields**](https://kettanaito.gitbooks.io/react-advanced-form/docs/getting-started/creating-fields.html). React Advanced Form is _field-centric_. That means you define flexible fields composites and reuse them throughout the entire application. Reflect even the most granular field state changes in the UI to achieve the outmost user experience.
* \*\*\*\*[**Prototyping speed**](getting-started/creating-form.md). Build production-ready forms at a speed of a prototype.

```jsx
// No, this is not a diminished example, this is a completely working form
<Form action={this.registerUser}>
  <Input name="username" required />
  <Input name="password" type="password" required />
</Form>
```

* [**Smart multi-layer validation**](https://kettanaito.gitbooks.io/react-advanced-form/docs/validation/logic.html). Declare even the most complex validation logic using single-line resolver functions.

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

Access the field's `value`, `fieldProps`, `fields` and the `form` as the parameters of each resolver function. Apply the rules application-wide via `FormProvider`, or extend/override them for a specific form. **Say goodbye to crowded** `validate` **functions, welcome clean validation schemas**!

* [**Reactive props**](https://kettanaito.gitbooks.io/react-advanced-form/docs/architecture/reactive-props.html). How much effort would it take you to make one field required based on another field\(s\)? Yes, the correct answer is—_one line of code_:

```jsx
<Input
  name="firstName"
  required={({ get }) => !!get(['lastName', 'value'])} />
<Input
  name="lastName"
  required={({ get }) => !!get(['firstName', 'value'])} />
```

Get as many data from the sibling fields as needed, and build your logic on that. Embrace the power of reactive programming, which re-evaluates a resolver function whenever the referenced field props update.

* [**Field grouping**](https://kettanaito.gitbooks.io/react-advanced-form/docs/components/Field.Group.html). Control the serialized data structure on the layout level by grouping the fields. Take advantage of split and nested groups.

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

The layout above serializes into the following JSON:

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

* **Third-party fields integration**. React Advanced Form can be used with **any** third-party fields library by using powerful [`createField`](hoc/create-field/) API.

### Getting started

#### Install

```bash
npm install react-advanced-form --save
```

> Make sure to have [React](https://github.com/facebook/react) \(15.0+\) installed in your project.

#### Guidelines

Starting with something new may appear challenging. There is a step-by-step instructions on how to get started with React Advanced Form, which ensure easy and clear integration process.

{% page-ref page="getting-started/installation.md" %}

### Resources

* [Documentation](https://kettanaito.gitbooks.io/react-advanced-form)
* [Advanced forms in React made easy](https://medium.com/@kettanaito/advanced-forms-in-react-made-easy-92a6e208f017) \(Medium\)

### Browser support

| Chrome | Firefox | Safari | iOS Safari | Edge | Internet Explorer |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 65+ | 57+ | 9+ | 8+ | 41+ | – |

> There is no official support for Internet Explorer. There is no testing conducted for that browser. Consider educating the web and deprecating support for obsolete browsers.

### Live examples

* [Synchronous validation](https://codesandbox.io/s/53wlvmp42l?module=%2Fsrc%2FSyncValidation.js)
* [Asynchronous validation](https://codesandbox.io/s/73236qlk06?module=%2Fsrc%2FAsyncValidation.js)

### Contributing

Any of your contributions are highly appreciated. See the [Contribution guidelines](https://kettanaito.gitbooks.io/react-advanced-form/docs/CONTRIBUTING.html) to get to know the process better. Moreover, development isn't the only way to contribute, there are [many more](https://kettanaito.gitbooks.io/react-advanced-form/docs/CONTRIBUTING.html#other-contributions).

