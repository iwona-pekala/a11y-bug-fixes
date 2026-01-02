# First dialog's interactive control should be automatically focused when a dialog is opened

When we consider that a control should be focused, it means:
- It should be focused for the keyboard.
- It should be focused for screen readers.

It's not possible to manually manage screen reader focus only, but once the keyboard focus is set, screen reader focus will follow as well.

What is your current dialog implementation?
1. [`role="dialog"`](#case-roledialog)
2. [`<dialog>`](#case-dialog-element)

## Case `role="dialog"`

Once the dialog is opened, use the [`focus()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/focus) method to move focus to the first interactive element in the dialog.
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

## Case `<dialog>`

Set the [`autofocus`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/autofocus) attribute on the first interactive element in the dialog.

```
<dialog aria-label="…">
<button autofocus>Close</button>
…
</dialog>
```
