# Dialog role

## Code
  An element is a dialog when:
  - It has an explicit dialog role

***Example:***

`<div role="dialog" aria-label="Upload attachments">…</div>`

***OR***
  - It has an implicit role derived from the `<dialog>` tag

***Example:***

`<dialog aria-label="Upload attachment">…</dialog>`

### Best practices
Do **NOT** apply the role twice:

`<dialog role="dialog">…</dialog>`

## Screen readers

- It's expected to hear 'dialog' when a dialog appears on the screen.

### Cases when 'dialog' may not be heard
- The dialog has no name
- Focus is not moved into the dialog when it's opened
- **TalkBack** screen reader has a bug that prevents dialog announcement
- Dialog is nested inside an element that doesn't allow dialog children
- The name was applied with a delay 
