# First dialog's interactive control should be automatically focused when a dialog is opened

When we consider that a control should be focused it means:
- It should be focused for keyboard.
- It should be focused for screen readers.

It's not possible to manually manage screen reader focus only, but once the keyboard focus is set, screen reader focus will follow as well.

What is your current dialog implementation?
1. [`role="dialog"`](#case-roledialog)
2. [`<dialog>`](#case-dialog-element)

## Case `role="dialog"`

Once the dialog is opened, use [`focus()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/focus) method to move focus to the first dialog's interactive element.
```
<div role="dialog" aria-label="…">
<button>Close</button>
…
</div>
```

```
<!-- Call when a dialog is displayed -->
…
closeButton.focus();
…
```

## Case `<dialog>` element

Set [`autofocus`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/autofocus) attribute on the first dialog's interactive element.

```
<dialog aria-label="…">
<button autofocus>Close</button>
…
</dialog>
```
