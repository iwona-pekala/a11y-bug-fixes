# Modal dialog

## Checklist

- The control that opens a dialog is a [button](../button/button-checklist.md)
- [Optional] [The control that opens a dialog indicates that it opens a dialog](dialog-entry-point-hint.md)
- When the dialog entry point is activated, keyboard focus moves into the dialog
  - [The first interactive element in the dialog receives focus](dialog-first-interactive-control-autofocus.md)
  - The focus indicator is visible
- Interactive components within the dialog can be operated using a keyboard
  - Each focused element has a visible focus indicator
  - Each focus indicator has sufficient color contrast
- Non-interactive elements inside the dialog cannot be reached using the Tab key
  - The dialog container itself cannot be reached using the Tab key
- Tabbing within the dialog does not allow focus to reach background elements
- Dialog can be closed with the Escape key
  - Inner components may handle the Escape key, but must prevent its default behavior when pressing Escape results in a visible UI state change. 
- [Dialog has a title](dialog-has-title.md)
- [When the dialog is closed, keyboard focus returns to the element that opened the dialog](dialog-focus-return.md)
- [Screen reader focus is trapped within the dialog](dialog-screen-reader-trap.md)
- [The dialog has the correct role](dialog-role.md)
- [The dialog has an accessible name](dialog-name.md)
