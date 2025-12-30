# Attributes which are redundant for a button
Some attributes added to the button won't impact accessibility, but they will blow up the code while not adding any value at all. **Most** of the items below **are applicable to the `<button>` tag**. Each section states the applicability explicitly.

## Role

If you use the `<button>` tag, do not add explicit role. The role is implicit in this case. In other words, the `<button>` has a role button by default.

**✖ BAD practice:**
```
<button role="button">Save</button>
```

**✔ Good practice:**
```
<button>Save</button>
```

## Name
Do not use `aria-label`/`aria-labelledby`/`title` if the button's name should match the text included inside the tag representing a button. This is applicable to both the native `<button>` *AND* **a custom button**.

**✖ BAD practices:**
```
<button aria-label="Save">Save</button>
<button aria-label="Save"><img src="…" alt="Save"></button>
<span tabindex="0" role="button" aria-label="Save">Save</button>
```

**✔ Good practices:**
```
<button>Save</button>
<button><img src="…" alt="Save"></button>
<span tabindex="0" role="button">Save</button>
```

## Tabindex
Do not `tabindex=0` to the native `<button>`. The `<button>` is keyboard focusable by default.

**✖ BAD practice:**
```
<button tabindex="0">Save</button>
```

**✔ Good practice:**
```
<button>Save</button>
```

## Key events
Do not add onkeydown / onkeyup to the native `<button>`. They are handled automatically for Enter/Space - onclick is executed.
