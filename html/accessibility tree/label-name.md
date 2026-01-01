# The difference between label and name

## What is element's label
Label is text (or an image of text) displayed on or next to the element, which describes its purpose.

### Other names of label
In accessibility context, label can be referenced as:
- Label
- Visible label

## What is name (accessibility name)
An element's name is text that is presented to assistive technologies, like screen readers.

### Other names of name
In accessibility context, name can be referenced as:
- Name
- Accessibility name
- Accessible name
- Accessibility label

## Referencing issue
As the same term can sometimes be called in a different way, it might be easy to confuse both of them. 

## Are label and name different?
While label and name are different terms, they are often created from the same element.
Visible text always acts as a label. At the same time visible text can, but doesn't have to act as a name.

If the name can be [created from content](https://www.w3.org/TR/wai-aria/#namefromcontent), and content is present, name is created automatically and in most cases there is no need to provide a name explicitly.

## Examples

### Button
A button can have a name created from content.
```
<!-- Save is used to create a name -->
<button>Save</button>
```

It's still possible to change such a name. This can be done using the `aria-label` attribute.
```
<!-- Now the button's name is "Save file", content is overwritten by aria-label  -->
<button aria-label="Save file">Save</button>
```

```
<!-- Now the button's name is "Store file" - this is bad practice as label is not included in name -->
<button aria-label="Store file">Save</button>
```

### Input
For elements for which labelling `<label>` tag is supported, and there are no attributes with higher priority when it comes to name computation, the `<label>` content acts as a name.
```
<!-- Input's name is "Year" - label's content -->
<label for="year">Year</label>
<input type="text" id="year"> 
```

It's still possible to override the visible text
```
<!-- Now the input's name is: "Current year"
aria-label and aria-labelledby have precedence over <label>
-->
<label for="year">Year</label>
<input aria-label="Current year" type="text" id="year"> 
```

### Dialog
Let's consider a similar example as before, but with a dialog.
```
<!-- There is some content, but dialog has no name, as dialog role doesn't support name from content -->
<dialog>
<span>Foo bar</span>
</dialog>
```

Still dialog needs to have a name, and the name must be [provided explicitly by the author](https://www.w3.org/TR/wai-aria/#namefromauthor).

```
<!-- Dialog's name is now "Foo bar" -->
<dialog aria-labelledby="title">
<span id="title">Foo bar</span>
</dialog>
```
