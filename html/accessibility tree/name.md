# Name (Accessibility name)

The accessibility name is the name of a user interface element. Name is used by assistive technologies, like screen readers.

## Name computation rules

Name computation rules are very complex and they are described in [Accessible Name and Description Computation 1.1](https://www.w3.org/TR/accname-1.1/#mapping_additional_nd_name).

### Sample calculation order for an element having textbox role (like `<input type="text">`)

1. Use the `aria-labelledby` attribute if present and valid, else
2. Use the `aria-label` attribute if present and valid, else
3. Use the `<label>` tag if present and valid, else
4. Use the `title` attribute if present and valid , else
5. Use the `placeholder` attribute if present and valid, else
6. Use the `aria-placeholder` attribute if present and valid, else
7. Name is the empty string.

### Sample calculation order for an element having button role (like `<button>`)
1. Use the `aria-labelledby` attribute if present and valid, else
2. Use the `aria-label` attribute if present and valid, else
3. Use the `<label>` tag if present and valid, else
4. Use the element's contents if present and valid, else
5. Use the `title` attribute if present and valid , else
6. Name is the empty string.

Name calculation precedence order may vary depending on role. The roughly valid order is:

`aria-labelledby` &gt; `aria-label` &gt; `<label>` (if applicable) &gt; contents (if applicable)
Precedence of the `title` attribute depends on context.

This section does not attempt to cover all possible scenarios.

## Name computation quirks
- [Not all elements can have supporting roles from the author](https://www.w3.org/TR/wai-aria/#namefromprohibited)
- [Not all elements can have supporting roles from content](https://www.w3.org/TR/wai-aria/#namefromprohibited)
- [Not all elements can be named](https://www.w3.org/TR/wai-aria/#namefromprohibited)
- For some elements names are required
- For some elements names are optional
