# Button has the correct role

Button's role must be: button.

## Implicit
The `<button>` tag provides implicit button role. There is no need to provide it explicitly.
```
<!-- Do NOT add button role here -->
<button>Save</button>
```

## Explicit
If any other tag is supposed to be perceived as a button, it needs a button role.
```
<span role="button">Save</span>
```

This is still far from an [accessible button](button-checklist.md). Several more steps are needed.
