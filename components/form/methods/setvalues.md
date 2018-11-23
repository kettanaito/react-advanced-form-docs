# setValues\(\)

Sets the values of the given fields.

## Definition

```typescript
type SetValues = (fieldsDelta: FieldsDelta) => void

type FieldsDelta = {
  [fieldPath: string]: any | FieldsDelta,
}
```

## Example

```jsx
import { Form } from 'react-advanced-form'
import { Input, Select } from 'react-advanced-form-addons'

export default class Example extends React.Component {
  handleSelectChange = () => {
    this.form.setValues({ foo: 'another' })
  }
  
  render() {
    return (
      <Form ref={form => this.form = form}>
        <Select onChange={this.handleSelectChange}>
          <option value="first">First</option>
          <option value="second">Second</option>
        </Select>
      
        <Input
          name="foo"
          initialValue="bar" />
      </Form>
    )
  }
}
```

