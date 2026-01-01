# How to break a native `<button>`'s accessibility?

While the `<button>` is mostly accessible by default. It still can be broken with 'techniques' below.

## Role

While the `<button>` has an implicit button role, it's still possible to remove it.

**✖ Do NOT do this**

```
<button role="none">Save</button>
<button role="presentation">Save</button>
<button role="link">Save</button>
<button role="navigation">Save</button>

<!-- Replace … with whatever, and the button is no longer a button -->
<button role="…">Save</button>
```

## Focusability
Any `<button>` can be reached with a Tab key. Still it can be broken by using `tabindex="-1"` attribute. Assuming that a button should be enabled and accessible in a standard way by everyone:

**✖ Do NOT do this**
```
<button tabindex="-1">Save</button>
```

## Focus indicator
Browsers provide the default focus indicator for each focusable element, including the `<button>`. 
- Do not add CSS that makes focus indicator not visible.
- Add own focus indicator if the default one is removed.

## Enter and Space
Any `<button>` with onclick event, can be activated with Enter and Space as well. Custom keyboard events for Enter/Space shouldn't be added. The outcome might be following:
- The button's action might be performed twice.
- The button might be impossible to activate with screen readers on.
- The button's action might be performed for any key. Example: The Tab key may activate the button

**✖ Do NOT do this**
```
<button onclick="save()" onkeydown="… save();" onkeyup="… save();" onkeypress="… save();">Save</button>
```

**✔ DO instead**
```
<button onclick="save()">Save</button>
```

## `click` event set for the correct element
As mentioned before providing onclick() is sufficient to ensure keyboard accessibility as well. However, `click` event must be set on the button, not on an inner or outer element.
Such a button will work with mouse without any issues, but cannot be activated with keyboard.

**✖ Do NOT do this**
```
<button><span onclick="save()">Save</span></button>
```

**✔ DO instead**
```
<button onclick="save()"><span>Save</span></button>
```
