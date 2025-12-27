# Modal dialog

## Checklist

- Dialog entry point is a button
  - [Optional] Dialog entry point indicates that it open a dialog
- When the dialog entry point is activated, keyboard focus moves into the dialog
  - The first interactive element in the dialog receives focus
  -The focus indicator is visible
- Interactive components within the dialog can be operated using a keyboard
  - Each focused element has a visible focus indicator
  - Each focus indicator has sufficient color contrast
- Non-interactive elements inside the dialog cannot be reached using the Tab key
  - The dialog container itself cannot be reached using the Tab key
- Tabbing within the dialog does not allow focus to reach background elements
- When the dialog is closed, keyboard focus returns to the element that opened the dialog
- Screen reader focus is trapped within the dialog
- [The dialog has the correct role](dialog-role.md)
- The dialog has an accessible name
