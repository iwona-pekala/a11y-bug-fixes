# Closing dialog with the Escape key

Users may expect that the dialog can be closed with the Escape key. This feature might be handy for all users, not all for users relying on assistive technologies. 
Unfortunately there might some issues with this behavior and it all depends the dialog's content. 
Assuming that a fully accessible dialog is created for an entire project, stiil there might be cases when the dialog's content will not work well with dialog's keyboard handling.

Jump directly to the implementation hints below if you are already familiar with the underlying constraints.
1. [`role="dialog"`](#case-roledialog)
2. [`<dialog>`](#case-dialog)

## Inner elements
The problem with the Escape key is: dialog's inner elements may handle the Escape key as well. All kind of autocompletes, tooltips which can be closed with the Escape key may interfere with the dialog. 
Unfortunately it's required handle the problem for each inner element and there seems to be no option to handle it on dialog's level.

### Custom widgets
All widgets that may be displayed inside the dialog and have Escape key event handlers should take it into account in the Escape key propagation.

### Native widgets
There are a few native HTML widgets which can display an extra element which can be closed The Escape key.

Elements which if placed inside the dialog can be closed with the Escape key in Chrome:
1. `<input type="text autocomplete="…">` - a text input with the `autocomplete` attribute - autocomplete list can be dismissed with the Escape key
2. `<input list="…>` - a text input with an autocomplete - autocomplete list can be dismissed with the Escape key
3. `<select>` - a list of option can be dismissed with the Escape key
4. `<input type="date">` - date picker can be dismissed with the Escape key
5. `<input type="date"  list="…">` - autocomplete list can be dismissed with the Escape key
6. `<input type="time">` - time picker can be dismissed with the Escape key
7. `<input type="time" list="…">` - autocomplete list can be dismissed with the Escape key
8. `<input type="color">` - color picker can be dismissed with the Escape key
9. `<input type="color" list="…">` - autocomplete can be dismissed with the Escape key
10. `<input type="file">` - file picker can be dismissed with the Escape key

After several optimistic case these is one which doesn't work as well.
#### `title`
The title attribute displays a hint over a hovered element. In this case Chrome dismisses the title and closes dialog at the same time. While not perfect, this scenario is less affecting keyboard only users, as titles are displyed on hover only, and they are not displayed on focus.

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
   - Yes - Fix the Escape key handling **AND** Allow dialog closing with the Escape key.
   - No - Disable dialog closing with the Escape key.
## Case `role="dialog"`
### Add Escape handling
The most popular [accessible dialog example](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/examples/dialog/) closes the dialog on `keyup` event, while native `<dialog>` is closed on `keydown` event. Picking the `keydown` allows to make the experience consistent, but it's minor details and most users won't notice the difference.
```
function closeDialog() {  
  dialog.className = "hidden";
}

dialog.addEventListener("keydown", (event) => {
  if (event.key === "Escape") {
    closeDialog();
  }
```

```
.hidden {
  display: none;
}
```
### Remove Escape handling
The Escape key won't work by default. No steps are required.

## Case `<dialog>`
### Add Escape handling
No extra steps are needed. Native modal dialog can be closed with the Escape key by default (`keydown` event).
### Remove Escape handling
Escape handler for the dialog can be removed with:
```
dialog.addEventListener("cancel", (event) => {
  event.preventDefault();
});
```
