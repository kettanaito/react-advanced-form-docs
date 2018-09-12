# Behavior

## Exclusive behavior

...

## Execution order

Understanding validation priority is crucial for crafting flexible validation logic.

1. Field.props.rule
2. Field.props.asyncRule
3. validationRules\[fieldName\]
4. validationRules\[fieldType\]

