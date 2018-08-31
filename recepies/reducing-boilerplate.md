# Utilizing functions

React Advanced Form encourages the usage of pure and high-order functions. These concepts can help you to reduce repetition and grant super powers during your forms declaration.

## High-order validators

Consider writing a set of pure high-order validator functions that accept optional set of parameters and always return a validator function expected by React Advanced Form:

```javascript
// validators/minLength.js
export default function minLength(length) {
    // returns a validator function expected by RAF
    return ({ value, fieldProps, fields, form }) => {
        return value.length >= length
    }
}
```

Now you can use the `minLength` function parametrically whenever necessary:

```javascript
// validation-rules.js
import minLength from './validators/minLength'

const validationRules = {
    type: {
        tel: {
            minLength: minLength(8)
        }
    },
    name: {
        firstName: {
            minLength: minLength(2)
        }
    }
}
```

