# Focus should return to the trigerring button when a dialog is closed

When we consider that a control should be focused it means:
- It should be focused for keyboard.
- It should be focused for screen readers.

It's not possible to manually manage screen reader focus only, but once the keyboard focus is set, screen reader focus will follow as well.

What is you current dialog implementation?
1. [`role="dialog"`](#case-roledialog)
2. [`<dialog>`](#case-dialog-element)

## Case `role="dialog"`
Once the dialog is closed, return focus using `focus()` method.

**Example:**
```
<button id="openButton">Open dialog</button>
```

```
// Once the dialog is closed
…
openButton.focus();
```

## Case `<dialog>` element
The modal was displayed by using showModal() method. Now it can be closed using `close()` method. Once it's done, focus will automatically return to the element which opened the dialog, as long as this element still exists and it's still focusable. There are no extra steps.

**Example:**
```
<dialog aria-label="…">
  <button autofocus>Close</button>
  …
</dialog>
<button>Open dialog</button>
```

```
openButton.addEventListener("click", () => {
  dialog.showModal();
});

closeButton.addEventListener("click", () => {
  dialog.close();
});
```
