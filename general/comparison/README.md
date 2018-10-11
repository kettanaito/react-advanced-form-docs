# Comparison

> **Why in the world do we need another form library?** — _A voice in the crowd._

Anything new emerges from the discontent with the present. The motivation for creating React Advanced Form is to challenge the expectations of a developer of what a form solution must do. We felt there are a lot of essentials missing in popular form solutions, and thus we have decided to implement our own.

## Overview

|   | Any form solution | React Advanced Form |
| :--- | :--- | :--- |
| **Design** | Form is a central point of implementation. | Field-centric. Any form is a composition of fields. |
| **Spectrum** | Focuses on simple use cases in favor of being smaller. | Focuses on complex use cases and has more responsibility in favor of maintainable code. |
| **Validation** | Doesn't include any validation algorithms. Delegates the logic to a developer.  | Includes smart multi-layer validation. Extendable, pluggable with any third-party validation library. |
| **Size** | Smaller. Requires extra code for any deviating use case. | **Bigger**. Close to no extra code for a scenario of any complexity. |

## Examples

There are three incrementally complex scenarios implemented using different form solutions to give you an overview of what to expect from React Advanced Form.

{% page-ref page="formik.md" %}

{% page-ref page="final-form.md" %}



