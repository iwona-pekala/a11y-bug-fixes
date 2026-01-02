# Native HTML widgets Escape key propagation

There are a few native HTML widgets which can display an extra content which can be closed The Escape key.
These widgets have been tested (in Chrome) in order to check if they stop Escape key propagation.

## Widgets that stop event propagation
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

## Widgets that do NOT stop event propagation
1. Any tag with the `title` attribute - The title attribute displays a hint over a hovered element. 


### Title note
While using an element with the `title` attribute inside another Escape dismissible element like a dialog may provide bad user exeperience, this scenario is less affecting keyboard only users, as titles are displyed on hover only, and they are not displayed on focus.
