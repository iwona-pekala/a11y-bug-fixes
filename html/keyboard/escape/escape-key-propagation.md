# Escape key propagation

Escape key is often used to dismiss/collapse/hide something. While implementing such a functionality may seem to be straight forward, embedding a control which can be closed with the Escape key inside another such element may create accessiblity issues for keyboard only users.

## Example
A custom text input with autocomplete is placed inside a modal dialog. Autocomplete options can be dismissed with the Escape key, so the dialog.
What happens when a user presses Escape in order to dismiss autocomplete options? It may happen that the entire dialog is closed, alongisde the almost completed long form.
Such a behavior might be annoying for all users (several users may try to use Escape in this case). Keyboard only users may simply not have another dismiss option.

## How to implement embeddable control with the Escape key handling

### Starting point
Intially the Escape handling can look like this:
```
widget.addEventListener("keydown", (event) => {
  if (event.key === "Escape") {
    <!-- A generic function that closes/collapses/dismisses something
    hide();
  }
});
```
The result is: what ever was displayed is no longer displayed, but the dialog is closed as well.

### Improved version
The Escape key propagation can stopped like this:
```
widget.addEventListener("keydown", (event) => {
  if (event.key === "Escape") {    
    hide();
    event.preventDefault();
  }
});
```
Now the dialog is not closed, and the dialog won't be closed as long as long the widget is focused, even if there is nothing to dismiss.

### Final version
The final version checks an extra content is hidden before an attempt to hide it again.
```
widget.addEventListener("keydown", (event) => {
  if (event.key === "Escape" && widgetExtraContent.hidden === false) {    
    hide();
    event.preventDefault();
  }
});
```
Final result:
1. When a widget with escape handling is focused and Escape is pressed, it's checked if there is something to dismiss.
   - If Yes, the dismissible content is dismissed, the dialog is NOT closed
   - If No, the dialog is closed
2. For all other focused controls, the dialogs Escape handling work as expected.

## Summary
While the dialog was used as an example, to allow easier understanding, the same approach can be applied to any other host element.
