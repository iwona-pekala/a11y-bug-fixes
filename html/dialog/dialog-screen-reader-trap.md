# Trapping screen reader focus inside a modal dialog

Screen reader is trapped inside the dialog, when all dialog's elements are accessibile for a screen reader, while any background page elements cannot be reached with a screen reader.

What is you current dialog implementation?
1. [`role="dialog"`](#1-case-roledialog)
2. [`<dialog>`](#2-case-dialog-element)

## 1. Case `role="dialog"`

If a dialog is implemented by using role=`dialog` attribute, screen reader focus can be trapped inside a dialog by using `aria-modal` property.

**Example:**

```<div role="dialog" aria-label="Upload files" aria-modal="true">…</div>```

### Screen readers
The one attribute above is sufficient for all screen readers except for TalkBack. TalkBack ignores aria-modal attribute. 

#### TalkBack resolution
There are two possible approaches: ignore TalkBack and wait for a full support, or provide a walkaround.
A walkaround involves seprating 'background' and the dialog's content and [hiding](../hiding/what-should-be-hidden.md) not relevant layer from screen readers.

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
## 2. Case `<dialog>` element
The modal <dialog> is displayed by using `showModal()` method. There are no extra steps required, screen reader focus is trapped inside such a dialog.

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
