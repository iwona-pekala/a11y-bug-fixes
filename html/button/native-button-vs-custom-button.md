# Native button vs. custom button

While it's possible to create a custom button which mimics the native `<button>`, this approach requires a lot of code and consideration. The experience shows, that something is always missing.

## `<button>`

The native `<button>` has very little requirements. It may occasionally need some tweaks. In most cases it's enough to leave it as it is and make as little modifications as possible. Let's imagine an empty page with a button:
```
<button onclick="save()">Save</button>
```

This button meets the criteria from the button checklist:
- ✔ Button has the correct role - `<button>` tag provides `button` role implicitly.
- ✔ Button has a name - "Save" text acts as a name.
- ✔ Button can be reached with the Tab key - `<button>` can be reached with the Tab key by default.
- ✔ Button has visible focus indicator - browsers provide visible focus indicator for a `<button>`.
- ✔ Button can be activated with Enter ***and*** Space keys - a `<button>` can be activated with Enter ***and*** Space keys by default. They both will call `onclick()`.
- ❓ Button is not used to navigate between URLs - By default the `<button>` doesn't do anything, but its behavior is almost always set, so this part can broken easily.
- ❓ Button's label describe its purpose - This part can be broken sometimes, as the label is always set by the developer. Assuming that the button above saves something, the label is fine.
- ✔ Button's label is included in its name - The button's label is 'Save', then name is also 'Save'. 'Save' is included in 'Save', so this criterion is met.

As we can see almost every checklist element is met by default without any extra effort.

## Custom button

Custom buttons are often created from an element without any semantics like: `<div>` or `<span>`, or from `<a>` tag.

### `<span>`
Let's assume that we want to meet the button checklist with the custom button created with `<span>`. Starting point is:
```
<span>Save</span>
```

#### Role
The `<button>` has implicit role, now we need to add a role explicitly. The span is turned into:
```
<span role="button">Save</span>
```
#### Name
The name will stay as "Save". No extra steps are needed.

#### Button can be reached with the Tab key
The `<button>` is focusable with the Tab key by default, but for `<span>` the `tabindex` attribute is needed:
```
<span role="button" tabindex="0">Save</span>
```
#### Button has visible focus indicator
This part was resolved by adding tabindex attribute.

#### Button can be activated with Enter ***and*** Space keys
There were no extra steps for the `<button>`. The onclick event handles also Space and Enter keys (onclick is called for Enter keydown and Space keyup). 

Custom button requires in addition to `onclick`:
- `onkeydown` for Enter (should perform the same action as `onclick`)
- `onkeyup` for Space (should perform the same action as `onclick`)
- `onkeydown` for Space. Space down scrolls a page by default, so this needs to be prevented to match a `<button>` behavior and to avoid really annoying behavior

```
<span id="b" role="button" tabindex="0" onclick="save()" onkeydown="if (event.key === 'Enter') save();" onkeyup="if (event.key === ' ') save();">Save</span>
```

```
document.getElementById("b").addEventListener("keydown", (e) => {
  if (e.key === " ") e.preventDefault();
});
```

#### Remaining checklist items
There are not extra steps to meet the remaining checklist criteria.
