# Dialog has a title

Dialog having a title is a good practice. A title is usually visible text at the top of the dialog.

**Example:**

```
<dialog aria-labelledby="dialog_title">
<h2 id="dialog-title">Upload files</h2>
…
</dialog>
```

## Considerations:
- Skipping visible title is not a failure.
- Dialog title being marked up as `<h2>` is often considered good practice, but it's not a must (other heading levels might be fine as well).
- Visible dialog's title is often linked with the dialog via `aria-labelledby`.
- If `aria-labelledby` points to the dialog's title, make sure that the title is not empty.
- Dialog title can be not visible, but accessible for screen reader users (off-screen heading).
- If the dialog title is present, in might be beneficiarry to use aria-labelledby over aria-label.
- If there is no text in DOM that can be considered a dialog's title, use aria-label to provide a name for the dialog.
