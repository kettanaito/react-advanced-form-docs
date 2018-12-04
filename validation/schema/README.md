# Validation schema

## Specification

Validation schema is a plain JavaScript Object with the keys representing field selectors, and the values—validation resolvers associated with them.

* \*\*\*\*[**Selector**](rule-definition.md#selector) is a key path that selects the field\(s\);
* \*\*\*\*[**Resolver**](rule-definition.md#resolver) is a pure function that returns the next validity state of the field\(s\);

Think of declaring validation rules as of applying CSS properties. To apply a CSS rule you first select the elements \(fields\), and then describe their properties \(rules\). Validation schema is designed with the same principle.

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

type Resolvable = RuleResolver | {[ruleName: string]: RuleResolver}
type RuleResolver = (params) => boolean
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
  * Named `hashsum` resolver that validates the hash-sum of the field's value.

## Priority & Exclusion

To get the most of the validation schema it's important to understand the priority and exclusion of the rules described in it. This is what powers the layered nature of a validation schema.

### Priority

Validation resolvers are executed with the following priority relevant to the selected fields \(listed from highest to lowest\):

1. **Synchronous validation**
   1. [`Field.props.rule`](../../components/field/props/rule.md)
   2. `schema.type[fieldProps.type]`
   3. `schema.name[fieldProps.name]`
2. **Asynchronous validation**
   1. [`Field.props.asyncRule`](../../components/field/props/async-rule.md)

Synchronous validation always precedes any asynchronous one, because it's meant to ensure a valid value format, while asynchronous validation validates the validity of the data. Combined with exclusion, you can rest assured that asynchronous validation operates on the valid format only.

### Exclusion

Exclusion is a characteristic of a validation schema that prevents some validation rules from being executed whenever a preceding rule rejects.

Take the next implementation as an example:

```jsx
import React from 'react'
import { Form } from 'react-advanced-form'
import { Input } from 'react-advanced-form-addons'

const emailsBlacklist = ['joe@doe.com']

const validationRules = {
  type: {
    email: ({ value }) => isValidEmail(value),
  },
  name: {
    userEmail: ({ value }) => !emailsBlacklist.includes(value),
  },
}

export default class ExclusionExample extends React.Component {
  validateEmail = ({ value }) => {
    return fetch('https://back.end/validate', {
      body: JSON.stringify(value),
    }).then((valid) => {
      return { valid }
    })
  }
  
  render() {
    return (
      <Form rules={validationRules}>
        <Input
          type="email"
          name="userEmail"
          initialValue="incorrect.email"
          asyncRule={this.validateEmail}
          required
        />
      </Form>
    )
  }
}
```

Example above declares three validation points \(application levels\):

1. Asserting the correct format of the `[type="email"]` fields;
2. Asserting the entered `[name="userEmail"]` is not in the blacklist;
3. Validating entered user e-mail against a backend;

Taking into account the invalid initial value of the `userEmail` field, the validation chain will look like:

| Status | Application level |
| :--- | :--- |
| [❌](https://emojipedia.org/cross-mark/)\(invalid format\) | `schema.type.email` |
| _skipped_ | `schema.name.userEmail` |
| _skipped_ | `asyncRule` |

If the value of the field becomes `joe@doe.com` \(valid format, but included in the blacklist\), the application layers will look like:

| Status | Application level |
| :--- | :--- |
| ✅\(valid format\) | `schema.type.email` |
| [❌](https://emojipedia.org/cross-mark/)\(in the blacklist\) | `schema.name.userEmail` |
| _skipped_ | `asyncRule` |

{% hint style="warning" %}
Each of these application levels is exclusive, meaning that whenever it rejects \(returns `false` as a field's next validity state\), the succeeding resolvers **will not be executed**.
{% endhint %}

## Applying schema

### Application-wide <a id="application-wide"></a>

We highly recommend to apply a validation schema application-wide.

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

A validation schema may be extended, or overridden, using the root-level `extend` property.

Once set to `true`, the current schema is deep merged with any higher-scope schema \(i.e. the one from `FormProvider`\). When set to `false`, the current schema will override any higher scope schema, and be used as-is.

```javascript
const validationRules = {
  extend: true, // extend any rules from the higher scope
  name: {
    myField: ({ value }) => (value !== 'foo'),
  },
}
```



