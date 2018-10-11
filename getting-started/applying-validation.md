# Applying validation

Once we have both [validation rules](validation-rules.md) and [messages](validation-messages.md) defined, we can to apply them to see the working result.

There are multiple ways to apply the validation to the forms in our application. Either of them are suitable in different situations.

## Application-wide

We can use a `FormProvider` component to apply the validation rules and message application-wide. That implies that all the forms in the application abide by the defined rules, which is what you want in most of the cases.

Render a `FormProvider` on the root level of your application, close to other providers you may have \(for example, from Redux or Apollo\).

```jsx
// app/index.js
import React from 'react'
import ReactDOM from 'react-dom'
import { FormProvider } from 'react-advanced-form'
import validationRules from './validation-rules'
import validationMessages from 'validation-messages'

const App = () => (
  <FormProvider rules={validationRules} messages={validationMessages}>
    <Root />
  </FormProvider>
)

ReactDOM.render(<App />, document.getElementById('root'))
```

## Form-wide

A validation schema can be applied to a specific form. By doing so, it can [extend or override](../validation/schema/#extending-a-schema) the application-wide schema on demand.

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

const validationRules = {
  extend: false, // when "true", merges custom- and application rules together
  type: {
    password: ({ value }) => anotherValidator(value),
  },
}

const validationMessages = {
  type: {
    password: {
      invalid: 'I am different than general invalid password message',
    },
  },
};

export default class ExampleForm extends React.Component {
  render() {
    return (
      <Form rules={validationRules} messages={validationMessages}>
        {/* ... */}
      </Form>
    )
  }
}
```

