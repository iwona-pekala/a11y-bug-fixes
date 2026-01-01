# Dialog name

## Code
A dialog **must** have an accessible name. A name can be added via the `aria-label` ***or*** `aria-labelledby` attribute. 

### `aria-label`
The `aria-label` content is a literal string that will be read by screen readers.

**`aria-label` examples:**

`<div role="dialog" aria-label="Upload files">…</div>`

`<dialog aria-label="Upload files">…</dialog>`

### `aria-labelledby`
The `aria-labelledby` content is the list of IDs of existing HTML tags. In the most common case, only one is referenced.

**`aria-labelledby` examples:**

```
<div role="dialog" aria-labelledby="dialog_heading">
  <h2 id="dialog_heading">Upload files</h2>
…
</div>
```

```
<dialog aria-labelledby="dialog_heading">
  <h2 id="dialog_heading">Upload files</h2>
…
</dialog>
```
### Best practices
Do not use `aria-label` and `aria-labelledby` at the same time. The `aria-labelledby` attribute has a higher priority when it comes to name computation, so `aria-label` will be ignored.

## Screen readers
Assuming that the element has the dialog role, it's expected to hear the name alongside the dialog announcement.

### Cases when a name cannot be heard
- The dialog has no role
- Focus is not moved into the dialog when it's opened
- **TalkBack** screen reader has a bug that prevents dialog announcement
- Dialog is nested inside an element that doesn't allow dialog children
- The name was applied with a delay
- There is a typo in the `aria-label` or `aria-labelledby` attribute
- IDs referenced inside `aria-labelledby` do not exist
- The dialog element is in the DOM and the element referenced inside `aria-labelledby` is part of the shadow DOM (or vice versa). 
