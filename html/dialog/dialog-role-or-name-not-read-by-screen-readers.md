# Dialog role / name troubleshooting steps
Follow the path below if role or name are not read by a screen reader or an incorrect name is read by the screen reader.

## Assistive technology support
1. Does the issue happen with some browsers/screen readers only?
   - If **No** - go the Role section
   - If **Yes** - go the next list item
2. Is it Android TalkBack or iOS VoiceOver?
   - If **Yes**
        - This is TalkBack issue only - If you are sure that no other screen readers are affected, then STOP. This is a bug in TalkBack, there is no workaround.
        - This is iOS VoiceOver, there is a role, no name, but at least role should be read. Add a name, VoiceOver doesn't read dialog role, when a name is missing.
     If **No** - Go to the Role section.

## Role
1. Find HTML for the dialog's container.
2. Is the container the `<dialog>` tag?
   - If **Yes** - go to the name section
   - If **No** - apply dialog role **AND** go to the Name section
3. Does the container have a `role="dialog"` attribute?
   - If **Yes** - go to the Name section
   - If **No** - apply dialog role **AND** go to the Name section
  
## Name
1. Does the container have `aria-label` or `aria-labelledby` attribute?
   - If **No** - [add aria-label or aria-labelledby attribute](dialog-name.md)
   - If **Yes, but there is a typo** - fix the typo. Retest. Start over if the issue persists.
   - If **Yes, but there are both `aria-label` and `aria-labelledby` present** - Remove one of them, aria-labelledby has precedence over aria-label. Retest. Start over if the issue persists.
   - If **Yes - aria-label only** - go to the aria-label section
   - If **Yes - aria-labelledby only** - go to the aria-labelledby section

### aria-label
1. Is aria-label value non-empty string matching the expected name
   - If **Yes** - TODO
   - If **No** - Update the value so it matches expected name
 ### aria-labelledby
1. Is aria-labelledby value non-empty string matching the expected name
   - If **Yes** - Replace aria-labelledby with aria-label **OR** replace a value with ids elements which show the expected dialog's name. Retest. Start over if the issue persists.
   - If **No** - Go to the next list item
2. Does aria-labelledby reference an existing id?
   - If **Yes** - Go to the next list item
   - If **No** - No. Add/update id of the element which contains dialog's name OR use aria-label instead.
3. Is there only one element with the referenced id
   - If **Yes** - Go to the next list item
   - If **No** - Update ids, make sure ids are unique
4. 
## Tricky cases
