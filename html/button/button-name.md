# Button has a name

An element with the button role must have a name.

A name for a button can be provided using:
1. `aria-labelledby` attribute
2. `aria-label` attribute
3. `<label>` tag
4. content
5. `title` attribute

The order listed above is not random. The name is computed in the order mentioned. When a condition is met (like when a given attribute, content, or tag is present), name computation stops and remaining name candidates are ignored.

## Content
While the content is low on the list, it's the element that is used very often. This is a very good name candidate, and there is no need to provide extra attributes.

**Examples:**
```
<button>Save</button>
<button><img src="" alt="Save"></button>
<span role="button" tabindex="0">Save</span>
<span role="button" tabindex="0"><img src="" alt="Save"></span>
```
In all cases above, the content provides a name, and in each case the name is "*Save*".

## No content or content without text alternatives

While the remaining naming options include: `aria-labelledby`, `aria-label`, `<label>`, and `title`, the most common use case for buttons is `aria-label`.

### `aria-label`
The `aria-label` attribute should contain the text that should act as a label. When picking `aria-label` content, imagine that this is a text that would be displayed on the button.

**Examples:**
```
<!-- Buttons with background image and no content -->
<button aria-label="Save"></button>
<span role="button" tabindex="0" aria-label="Save"></span>

<!-- Buttons with content without a text alternative -->
<button aria-label="Save"><img src="" alt=""></button>
<span role="button" tabindex="0" aria-label="Save"><img src="" alt=""></span>
```

**✖ Antipatterns**

Do not add `aria-label` that duplicates content.
```
<button aria-label="Save"><img src="" alt="Save"></button>
<span role="button" tabindex="0" aria-label="Save">Save</span>
```
