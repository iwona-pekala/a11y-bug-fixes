# Description (accessibility)

Accessibility description (accessible description) is additional information about the component, which might be provided alongisde the [name](name.md).
Description cannot replace the name, it's always suplemental.

## Description computation rules
Description computation rules are described in:
- [Accessible Name and Description Computation 1.1 (W3C recommendation)](https://www.w3.org/TR/accname-1.1/#mapping_additional_nd_description)

Work on the new version is in progress:
- [Accessible Name and Description Computation 1.2 (W3C working draft)](https://www.w3.org/TR/accname-1.2/#mapping_additional_nd_description)

## Calculation order
While description calculation is less complicated than name calculation, it still might be confusing.

### Working draft order

1. `aria-describedby`
2. `aria-description`
3. HTML features
   - `<caption>` for `<table>`, but only if caption wasn't used as a name
   - `<summary>` for `<details>`, but only if it wans't used as a name
   - `value` for <`input>` with `type`s: `button`, `submit`, `reset`, but only if it wasn't used as a name
4. `title` attribute for any tag, but only if it wasn't used as a name

#### `aria-description` note
The `aria-description` attribute is still a part of draft documents, but regardless it has [very good browser support](https://caniuse.com/?search=aria-description).
