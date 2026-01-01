# Button's label is included in its name

## Label and name definitions
- Label - text displayed on the button (image of text counts as well).
- [Name](../accessibility%20tree/name.md) - text presented to assistive technologies.

Details about [label and name](label-name.md) are described in the accessibility tree chapter.

## Why?
While most accessibility tree properties are mostly intended for screen readers, but **label in name** check is intended for speech input users (users who control their devices using voice).

This check comes directly from [WCAG 2.5.3 success criterion](https://www.w3.org/WAI/WCAG22/Understanding/label-in-name.html).
It's defined to ensure that speech input assistive technologies can activate controls using their visible text.

## How it works?
When a speech input hears activation command followed by a keyword, it tries to find a control which name contains a spoken keyword. Users are likely to say labels seen on or near the control, and they can't guess the name if it doesn't contain visible text.

## What "contains" mean

Simplified formula:
1. Identify element's label (visible text that might be considered a label by users).
2. Remove punctuation and capitalization.
3. Identify element's name.
4. Remove punctuation and capitalization.
5. Check if string found at step 2 is included in step found at step 4.
   - Copy the string found at step 2 into a Notepad.
   - Copy the string found at step 4.
   - Press ctrl+f, search for the last copied string.
   - Check if the string is found.
7. If YES, then "label in name" is met.

## When in doubt
- Make the name matching label exactly
- If you need to update a name to make sure it describes control's purpose:
  - Copy label and append additional information after it.
- Test with speech input assistive technologies.

## Examples ##

### Label in name met

```
<!-- Name matches visible text ("Find") -->
<button>Find</button>
```

```
<!-- "Find" label is included in "Find images" name -->
<button aria-label="Find images">Find</button>
```

```
<!-- Name matches visible text ("Search files"), description provided via aria-describedby doesn't affect the name -->
<button aria-describedby="desc">Search files</button>
<span id="desc">This feature works for private files only</span>
```

### Label in name NOT met

```
<!-- Label "Find" is NOT included in "Search" name -->
<button aria-label="Search">Find</button>
```

```
<!-- Label "Find a file" is NOT included in "Find file" name -->
<button aria-label="Find file">Find a file</button>
```

```
<!-- Label "Search files" is NOT included in "This feature works for private files only."
Additionally the name doesn't describe the button's purpose, so screen reader users are affected as well.
-->
<button aria-labelledby="desc">Search files</button>
<span id="desc">This feature works for private files only.</span>
```
