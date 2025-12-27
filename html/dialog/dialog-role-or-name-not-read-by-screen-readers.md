# Dialog role or name is not read by a screen reader - troubleshooting steps

## Role

1. Find HTML for the dialog's container.
2. Is the container the `<dialog>` tag?
   - If **Yes** - go to the name section
   - If **No** - apply dialog role **AND** go to the name section
3. Does the container have a `role="dialog"` attribute?
   - If **Yes** - go to the name section
   - If **No** - apply dialog role **AND** go to the name section
  
## Name
