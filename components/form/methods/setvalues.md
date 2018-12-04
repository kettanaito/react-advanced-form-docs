# setValues\(\)

Sets the values of the given fields.

This method is designed to update the fields values during the runtime without making the fields controlled explicitly. **You must not invoke `setValues()` on controlled fields.**

## Definition

```typescript
type SetValues = (fieldsDelta: FieldsDelta) => void

type FieldsDelta = {
  [fieldPath: string]: any | FieldsDelta,
}
```

## Example

Call the `formRef.setValues()` with the Object as its argument. Each key in that Object represents a field path, and each value either the next same Object, or the next value of the selected field.

```jsx
import React from 'react'
import { Form, Field } from 'react-advanced-form'
import { Input, Select } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleCustomerTypeChange = () => {
    this.formRef.setValues({
      foo: 'another',
      primaryInfo: {
        firstName: 'John',
        lastName: 'Mavericl',
    })
  }
  
  render() {
    return (
      <Form ref={form => this.formRef = form}>
        <Select onChange={this.handleCustomerTypeChange}>
          <option value="b2c">Private</option>
          <option value="b2b">Business</option>
        </Select>
      
        <Input type="email" name="email" />
        <Input type="password" name="password" />
        
        <Field.Group name="primaryInfo">
          <Input name="firstName" />
          <Input name="lastName" />
        </Field.Group>
      </Form>
    )
  }
}
```

