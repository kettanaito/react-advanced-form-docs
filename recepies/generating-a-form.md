# Generating a form

Certain implementations rely on generating a form based on some data \(i.e. a JSON\). You can use React Advanced Form and generate the forms dynamically, however, there is no pre-built solution exposed to you.

### Reasoning

Assuming the logic of the fields/form generation should not be a form's concern. Writing a simple generating function that returns React components \(fields\) is a rather trivial procedure.

```jsx
import * as fields from './fields'

/**
 * Return the generated form based on the provided JSON
 * that describes the fields of a form.
 */
function generateForm(props, fieldsJson) {
  return (
    <Form {...props}>
      {generateFields(fieldsJson)}
    </Form>
  )
}

function generateFields(fieldsJson) {
  return fieldsJson.map((fieldParams) => {
    const { fieldType, ...props } = fieldParams
    const Field = fields[fieldType]
    
    return (
      <Field {...props} />
    )
  })
}

export default GeneratedForm extends React.Component {
  registerUser = ({ serialized }) => {}
  
  render() {
    const { fieldsJson } = this.props
    
    return generateForm({
      action: this.registerUser,
    }, fieldsJson)
  }
}
```

The usage of such a component would look as follows:

```jsx
<GeneratedForm
  fieldsJson={
    [
      {
        fieldType: 'Input',
        name: 'username',
        initialValue: 'john.maverick@email.com',
        required: true,
      },
      {
        name: 'password',
        fieldType: 'Select',
        type: 'password',
        required: true,
      },
    ]
  }
/>
```

The contract between your JSON and the generating function is up to you.

