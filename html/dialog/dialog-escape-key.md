# Closing dialog with the Escape key

Users may expect that the dialog can be closed with the Escape key. This feature might be handy for all users, not all for users relying on assistive technologies. 
Unfortunately there might some issues with this behavior and it all depends the dialog's content. 
Assuming that a fully accessible dialog is created for an entire project, stiil there might be cases when the dialog's content will not work well with dialog's keyboard handling.

## Inner elements
The problem with the Escape key is: dialog's inner elements may handle the Escape key as well. All kind of autocompletes, tooltips which can be closed with the Escape key may interfere with the dialog. 
Unfortunately it's required handle the problem for each inner element and there seems to be no option to handle it on dialog's level.

### Custom widgets
All widgets that may be displayed inside the dialog (or other widget which interacts with the Escape key) should take it into account in the Escape key handling function.

### `autocomplete`
When dialog's element is an input with the `autocomplete` attribute, the autocomplete options are handled by the browser. Luckily browsers (Chrome at least) hide the autocomplete list without propagating the Escape key.
TODO

## Escape or no Escape
When deciding if the dialog template used across a (big) project should be possible to close with the Escape key, it might be required to consider if it's possible to predict what kind of elements might be displayed inside the dialog.

### Decission steps
1. Will dialog host elements which will be dismissible with the Escape key?
   - Yes **OR** Hard to tell - Continue.
   - No - Allow dialog closing with the Escape key.
2. Will the componenets guarantee correctly used `preventDefault()`
   - Yes - Allow dialog closing with the Escape key.
   - No - Continue.
3. Will you be able to fix the Escape handling for all dialog's inner elements?
   - Yes - Fix the Escape key handling AND Allow dialog closing with the Escape key.
   - No - Disable dialog closing with the Escape key.
## Case `role="dialog"`
```
function closeDialog() {  
  dialog.className = "hidden";
}

dialog.addEventListener("keydown", (event) => {
  if (event.key === "Escape") {
    closeDialog();
  }
```

## Case `<dialog>`
No extra steps are needed. Native modal dialog can be closed with the Escape key by default (`keydown` event).
This behavior might be prevented with:
```
dialog.addEventListener("cancel", (event) => {
  event.preventDefault();
});
```
