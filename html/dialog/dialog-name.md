# Dialog name

## Code
A dialog **must** have an implicit name. A name can be added via aria-label ***or*** aria-labelledby attributes. 

### aria-label
The aria-label content is a literal string that will be read by screen readers.

**aria-label examples:**

`<div role="dialog" aria-label="Upload files">…</div>`

`<dialog aria-label="Upload files">…</dialog>`

### aria-labelledby
The aria-labelledby content is the list of ids of existing HTML tags. In the most common case one is referenced.

**aria-labelledby examples:**

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
Do not use aria-label and aria-labelledby at the same time. The aria-labelledby attribute has a higher priority when it comes to name computing, aria-label will be ignored.

## Screen readers
Assuming that the element has dialog role, it's expected to hear name alongside the dialog announcement.

### Cases when a name cannot be heard
- The dialog has no role
- Focus is not moved into dialog when it's opened
- **TalkBack** screen reader has a bug which prevents dialog announcement
- Dialog is nested inside an element which doesn't allow dialog children
- Name was applied with a delay 
