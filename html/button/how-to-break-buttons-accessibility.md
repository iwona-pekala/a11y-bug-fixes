# What can go wrong with button's accessibility

## Role

### Random non-`<button>` tag pretending to be a button
**✖ Broken example:**
```
<span onclick="action()">I'm pretending to be a button</span>
```

**✔ DO instead:**
Preferred:
```
<button>I'm a button</button>
```

Last resort with several extra conditions:
```
<span onclick="action()" role="button" …>I'm pretending to be a button</span>
```

### A <button> tag with role attribute
Almost any role added to the `<button>` tag will strip the button's role. The only exception is `role="button"`, but there is no point of indicating that button is a button.

**✖ Broken example:**
```
<button role="none">Confirm</button>

<!--
The tag below is an eqivalent of writing the sam code twice, like this:
i = 0;
i = 0;
-->
<button role="button">Confirm</button>
```

**✔ DO instead:**
```
<button>Confirm</button>
```

#### Exceptions
While applying a new role will strip the original role, there might be cases when it's intended. Some tab panel implementations may include elements like: `<button role="tab">`, but if you are about to change button's role, make sure it's *really* intended.

### `<a role="button">`
TODO

## Name

### Missing name
### Name that doesn't describe the purpose
### Inconsistent name
### Label not included in name

## Button is not keyboard focusable

## Keyboard activation

### Space doesn't activate the button
### Enter doesn't activate the button
### Keyup or Keydown
### onclick set for an incorrect tag
### Works with keyboard only, but doesn't work with a screen reader
### Page scrolls when space is pressed

## No focus indicator

## Button used to navigate between URLs
