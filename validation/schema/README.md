# Validation schema

## Specification

Validation schema is a plain JavaScript Object of a defined shape that consists of selectors and resolvers associated with them.

* \*\*\*\*[**Selector**](rule-definition.md#selector) is a key path that selects the field\(s\),
* \*\*\*\*[**Resolver**](rule-definition.md#resolver) is a pure function that returns the next validity state of the field\(s\).

## Definition

```typescript
type ValidationSchema = {
  extend?: boolean,
  type?: {
    [fieldType: string]: Resolvable,
  },
  name?: {
    [fieldName: string]: Resolvable,
  },
}

type Resolvable = Resolver | {[ruleName: string]: Resolver}

type Resolver = (params) => boolean
```

## Declaration

Here is an example of a simple validation schema:

```javascript
export default {
  type: {
    password: ({ value }) => value.length > 6,
  },
  name: {
    vatNumber: {
      format: ({ value }) => /^\d{8}$/.test(value),
      hashsum: ({ value }) => value[2] + value[5] === 12,
    },
  },
}
```

There are a few resolvers applied in the schema above:

* For all fields of `[type="password"]`:
  * Anonymous resolver that validates a field's value length.
* For all fields of `[name="vatNumber"]`:
  * Named `format` resolver that validates the format of the field's value,
  * Named `hashsum` resolver that validated the hash-sum of the field's value.

## Priority & Exclusion

Validation resolvers are executed with the following priority relevant to the applied field \(from highest to lowest\):

1. Synchronous validation:
   1. [`Field.props.rule`](../../components/field/props/rule.md)
   2. `schema.name[fieldName]`
   3. `schema.type[fieldType]`
2. Asynchronous validation:
   1. [`Field.props.asyncRule`](../../components/field/props/async-rule.md)

{% hint style="warning" %}
Each of these application levels is exclusive, meaning that when it rejects \(returns `false` as the next validity state\), the succeeding validators will **not** be executed.
{% endhint %}

## Applying schema

### Application-wide {#application-wide}

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import { FormProvider } from 'react-advanced-form'
import Root from './Root'
import validationRules from './validation/rules'

const App = () => (
  <FormProvider rules={validationRules}>
    <Root />
  </FormProvider>
)

ReactDOM.render(<App />, document.getElementById('root'))
```

### Form-wide

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'

const validationRules = {
  extend: true,
  name: {
    username: ({ value }) => !blacklist.includes(value),
  },
}

export default class ExampleForm extends React.Component {
  render() {
    return (
      <Form rules={validationRules}>
        {/* Fields */}
      </Form>
    )
  }
}
```

## Extending a schema

A validation schema may be extended or overridden using a root-level `extend` option.

Once set to `true`, the current schema is deep merged with any higher scope schema \(i.e. the one from `FormProvider`\). When set to `false`, the current schema will override any higher scope schema.

```javascript
const validationRules = {
  extend: true, // extend any rules from the higher scope
  name: {
    myField: ({ value }) => (value !== 'foo'),
  },
}
```



