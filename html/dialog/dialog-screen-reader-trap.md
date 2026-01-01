# Trapping screen reader focus inside a modal dialog

A screen reader is trapped inside the dialog when all dialog elements are accessible to a screen reader, while any background page elements cannot be reached with a screen reader.

What is your current dialog implementation?
1. [`role="dialog"`](#case-roledialog)
2. [`<dialog>`](#case-dialog-element)

## Case `role="dialog"`

If a dialog is implemented by using the `role="dialog"` attribute, screen reader focus can be trapped inside a dialog by using the `aria-modal` property.

**Example:**

```<div role="dialog" aria-label="Upload files" aria-modal="true">…</div>```

The one attribute above is sufficient for all screen readers except for TalkBack. TalkBack ignores the `aria-modal` attribute. 

### TalkBack resolution
There are two possible approaches: ignore TalkBack and wait for full support, or provide a workaround.
A workaround involves separating 'background' and the dialog's content and [hiding](../hiding/what-should-be-hidden.md) the irrelevant layer from screen readers.

**Example:**

```
<body>
  <!-- An element or set of elements of the 'background' -->
  <!-- Should be hidden when a dialog is opened -->
  <!-- Should be accessible when a dialog is NOT opened -->
  <div> 
    …
  </div>

  <!-- Dialog content placed outside the 'background' tags -->
  <!-- Should be accessible when a dialog is opened -->
  <!-- Should be hidden when a dialog is NOT opened -->
  <div role="dialog" aria-label="…" …>
    …
  </div>
</body>
```
## Case `<dialog>` element
The modal `<dialog>` is displayed by using the `showModal()` method. There are no extra steps required; screen reader focus is trapped inside such a dialog.

**Example:**

```
<button>Open dialog</button>
<dialog aria-label="…">
  …
</dialog>
```

```
showButton.addEventListener("click", () => {
  dialog.showModal();
});
```
