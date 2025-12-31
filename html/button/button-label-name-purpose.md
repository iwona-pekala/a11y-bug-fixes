# Button's label and name describe its purpose

As labels are visible in most cases they describe control's purpose. However this check is still very subjective. 
When it comes to names, it's easy break them, for example by providing suplementary information as a name. 

When determining if a name describes the purpose, imagaine that you just hear it without seeing it.

## Example
```
<button>This is me</button>
```

Imagine a `<button>` which has a label (visible text): "This is me". The button is displayed at the bottom of the screen on which a user can create own avatar (decide on: hair color, hair lenght, nose shape, eye color, etc.).
For sighted users a label "This is me" is likely clear. The button has an no explicit name provided by the author, so "This is me" text is used as a name as well. 

Now let's consider screen reader users. They will hear exactly the same text as sighted users will see. Still, some of them may not understand what it means, as they can't see the entire screen at once.
The above examples is based on a real survey reply from a blind user.

The fix may include providing some extra information in the name:
```
<button aria-label="This is me. Confirm my avatar's look">This is me</button>
```

In the fixed version, the name is provided via aria-label attribute. The name contains visible text *AND* provides extra information.
Visible text (label) must be included in name.

## Resolving subjectivy
In cases of any doubts about button's purpose, it's better to provide cleared version.
The best option to find out problematic labels/names is conducting surveys with real users.
