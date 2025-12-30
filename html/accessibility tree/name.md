# Name (accessibility)

The name is a human-readable text alternative that identifies a user interface component.

## Name computation rules

Name computation has complex rules described in [Accessible Name and Description Computation 1.1](https://www.w3.org/TR/accname-1.1/#mapping_additional_nd_name).

### Sample calculation order for an with having textbox role (like `<input type="text">`

1. Use aria-labelleby if present and valid, else
2. Use aria-label if present and valid, else
3. Use <label> if present and valid, else
4. Use title attribute if present and valid , else
5. Use placeholder if present and valid, else
6. Use aria-placeholder if present and valid, else
7. Name is the empty string.
