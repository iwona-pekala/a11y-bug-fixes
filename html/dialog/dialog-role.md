# Dialog role

## Code
  An element is a dialog when:
  - It has an explicit dialog role

***Example:***

`<div role="dialog" aria-label="Upload attachments">…</div>`

***OR***
  - It has implicit role derived from the `<dialog>` tag

***Example:***

`<dialog aria-label="Upload attachment">…</dialog>`

### Best practices
Do **NOT** not apply the role twice:

`<dialog role="dialog">…</dialog>`

## Screen readers

- It's expected to hear 'dialog', when a dialog appears on the screen.

### Cases when 'dialog' may not be heard
- The dialog has no name
- Focus is not moved into dialog when it's opened
- **TalkBack** screen reader has a bug which prevents dialog announcement
- Dialog is nested inside an element which doesn't allow dialog children
- Name was applied with a delay 
