# Utilizing functions

React Advanced Form encourages to use pure and high-order functions to significantly reduce repetition.

## High-order validators

Consider writing a set of pure high-order validator functions that accept optional set of parameters and always return a validator function expected by React Advanced Form:

{% code-tabs %}
{% code-tabs-item title="validators/minLength.js" %}
```javascript
export default function minLength(length) {
    // returns a validator function expected by RAF
    return ({ value, fieldProps, form }) => {
        return value.length >= length
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Use the `minLength` function parametrically whenever necessary:

{% code-tabs %}
{% code-tabs-item title="validationRules.js" %}
```javascript
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
{% endcode-tabs-item %}
{% endcode-tabs %}

