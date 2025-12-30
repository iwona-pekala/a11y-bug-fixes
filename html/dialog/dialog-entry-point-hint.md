# A control that opens a dialog

A control which is used to open a dialog should be a [button](../button/button-checklist.md).

## Indicate that a button opens a dialog
Indicating that a button opens a dialog is optional but it can be done by using `aria-haspopup="dialog"` attribute.

**Examples:**

```<button aria-haspopup="dialog">Upload files</button>```

```<span role="button" tabindex="0" aria-haspopup="dialog">Upload files</button>```

### Anti-pattern
Never use value other than `dialog` for `aria-haspopup` for a button which opens a dialog.
The apparently generic value `true` indicates a menu.

***BAD examples:***

```<button aria-haspopup="true">Upload files</button>```

```<span role="button" tabindex="0" aria-haspopup="true">Upload files</button>```

## Screen readers
Screen reader announcements will include phrases like: "has popup", "has popup dialog", "opens dialog".
