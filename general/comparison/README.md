# Comparison

> **Why in the world do we need another form library?** — _A voice in the crowd._

Anything new emerges from the discontent with the present. The motivation for creating React Advanced Form is to challenge the expectations of a developer of what a form solution must do. We felt there are a lot of essentials missing in popular form solutions, and thus we have decided to implement our own.

## Overview

|   | React Advanced Form | Another solution |
| :--- | :--- | :--- |
| **Focus** | Field-centric. Treats any form as a composition of fields. | Form is usually a central point of implementation. |
| **Motivation** | Focuses on complex use cases, and has more responsibility in favor of maintainable code. | Focuses on simple use cases in favor of being smaller. |
| **Validation** | Includes smart multi-layer validation. Extendable, composable, pluggable with any third-party validation library. | Doesn't include any validation algorithms. Delegates the logic to a developer.  |
| **Size** | **Bigger**. Close to no extra code for a scenario of any complexity. | **Smaller**. Requires extra code for any deviating use case. |

## Bundle size

We are transparent about the cost of adding a new dependency into your application. Regardless of any future optimizations, React Advanced Form will most likely remain _bigger_ than any other form package.

Choosing a package is a question of balance between the dependency size you introduce, and the features you get shipped. A smaller library that requires to write additional code to cover basic scenarios has much bigger effect on the size of your application, than deciding on a heavier solution that results into less code on your side.

Please see the minified bundle size comparison with popular form solutions below.

## Examples

There are three incrementally complex scenarios implemented using different form solutions to give you an overview of what to expect from React Advanced Form.

{% page-ref page="formik.md" %}

{% page-ref page="final-form.md" %}



