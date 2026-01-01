# Button's name doesn't include role

Name and role are separate elements. Duplicating role in a name is bad practice. This results in double announcement from screen readers.
Button announcement comes from implicit (`<button>`) or explicit (`role="button"`) role.

## Bad examples

```
<!-- Screen reader output: Save button button -->
<button aria-label="Save button">Save</button>

<!-- Screen reader output: Save button button -->
<span role="button" tabindex="0" aria-label="Save button">Save</span>

<!-- Screen reader output: Save button button -->
<input type="button" value="Save" aria-label="Save button">

<!-- Screen reader output: Button button -->
<button aria-label="button">Save</button> 
```

## Good examples

```
<!-- Screen reader output: Save button -->
<button>Save</button>

<!-- Screen reader output: Save button -->
<span role="button" tabindex="0">Save</span>

<!-- Screen reader output: Save button -->
<input type="button" value="Save">
```
