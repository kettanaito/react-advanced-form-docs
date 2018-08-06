# Reducing boilerplate

React Advanced Form encourages pure functions and high-order functions. Those can help you tremendously to reduce the repetition in your forms and validation rules.

## High-order validator functions

Consider writing a set of pure high-order validator functions that accept any custom parameters and always return a validator function expected by React Advanced Form:

```javascript
// validators/minLength.js
export default function minLength(length) {
    // returns a validator function expected by RAF
    return ({ value, fieldProps, fields, form }) => {
        return value.length >= length
    }
}
```

Now you can use the minLength function in multiple places:

```javascript
// validation-rules.js
import minLength from './validators/minLength'

const validationRules = {
    type: {
        tel: {
            // phones must be at least 8 characters long
            minLength: minLength(8)
        }
    },
    name: {
        firstName: {
            // first name must be at least 2 chars long
            minLength: minLength(2)
        }
    }
}
```

