# Button has a name

Element having button role must have a name.

A name for a button can be provided using:
1. `aria-labelledby` attribute
2. `aria-label` attribute
3. `<label>` tag
4. content
5. `title` attribute

The order listed above is not random. Name is computed in the order mentioned. When a condition is met (like: given attribute,content or tag is present). Name computation stops and remaining name candidates are ignored.

## Content
While the content is low on the list, it's the element which is used very often. This is a very good name candidate and there is no need to provide extra attributes.

**Examples:**
```
<button>Save</button>
<button><img src="" alt="Save"></button>
<span role="button" tabindex="0">Save</span>
<span role="button" tabindex="0"><img src="" alt="Save"></span>
```
In all cases above the content provides a name and in both cases the name is "*Save*".

## No content or content without text alternatives

While the remaining naming options include: `aria-labelledby`, `aria-label`, `<label>`, and `title`, the most common use case for buttons is `aria-label`.

### aria-label
The aria-label attribute should contain the text that should act as a label. When picking aria-label content, imagine that this is a text that would be displayed on the button.

**Examples:**
```
<!-- Buttons with background image and no content -->
<button aria-label="Save"></button>
<span role="button" tabindex="0" aria-label="Save"></span>

<!-- Buttons with with contents not having text alternative -->
<button aria-label="Save"><img src="" alt=""></button>
<span role="button" tabindex="0" aria-label="Save"><img src="" alt=""></span>
```

**✖ Antipatterns**
Do not add aria-label which duplicates content
```
<button aria-label="Save"><img src="" alt="Save"></button>
<span role="button" tabindex="0" aria-label="Save">Save</span>
```
