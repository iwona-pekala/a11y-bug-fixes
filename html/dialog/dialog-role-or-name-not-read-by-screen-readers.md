# Dialog role / name troubleshooting steps
Follow the path below if role or name are not read by a screen reader or an incorrect name is read by the screen reader.

## First steps
1. Find HTML for the dialog's container.
## Assistive technology support
1. Does the issue happen with some browsers/screen readers only?
   - If **No** – Go the [Role](#role) section
   - If **Yes** – Continue
2. Is it Android TalkBack or iOS VoiceOver?
   - If **Yes**, this is TalkBack issue only – If you are sure that no other screen readers are affected, then this is a bug in TalkBack, there is no workaround. Stop.
   - If **Yes**, this is iOS VoiceOver **AND** there is a role **AND** the role is not read **AND** There is no name – Add a name, VoiceOver doesn't read dialog role, when a name is missing. Retest. Go to the [Role](#role) section if the issue persists.
   - If **No** – Go to the [Role](#role) section.
## Role
1. Is the container the `<dialog>` tag?
   - If **Yes** – Continue
   - If **No** – Apply dialog role **AND** go to the [Name](#name) section
2. Does the <dialog> tag have `role` attribute?
   - If **Yes** - `role="dialog"` – If it wasn't added as a workaround for a browser/screen reader not supporting <dialog> - remove it. Go to the [Name](#name) section.
   - If **Yes** - `role` value is other than `dialog` – remove the role attribute entirely. Retest. Go to the [Name](#name) section if the issue persists.
   - If **No** – go the [Name](#name) section
3. Does the non <dialog> container have a `role="dialog"` attribute?
   - If **Yes** – Go to the [Name](#name) section
   - If **No** – Apply dialog role **AND** Continue  
## Name
1. Does the container have `aria-label` or `aria-labelledby` attribute?
   - If **No** – [Add aria-label or aria-labelledby attribute](dialog-name.md)
   - If **Yes, but there is a typo** – Fix the typo. Retest. Start over if the issue persists.
   - If **Yes, but there are both `aria-label` and `aria-labelledby` present** – Remove one of them, aria-labelledby has precedence over aria-label. Retest. Start over if the issue persists.
   - If **Yes - aria-label only** – Go to the [aria-label](#aria-label) section
   - If **Yes - aria-labelledby only** – Go to the [aria-labelledby](#aria-labelledby) section
### aria-label
1. Is aria-label value non-empty string matching the expected name
   - If **Yes** – Go to [Tricky cases](#tricky-cases) section
   - If **No** – Update the value so it matches expected name. Retest. Start over if the issue persists.
### aria-labelledby
1. Is aria-labelledby value non-empty string matching the expected name
   - If **Yes** – Replace aria-labelledby with aria-label **OR** replace a value with ids elements which show the expected dialog's name. Retest. Start over if the issue persists.
   - If **No** – Continue
2. Does aria-labelledby reference an existing id?
   - If **Yes** – Continue.
   - If **No** – Add/update id of the element which contains dialog's name **OR** use aria-label instead. Retest. Start over if the issue persists.
3. Is there only one element with the referenced id?
   - If **Yes** – Continue
   - If **No** – Update ids, make sure ids are unique. Retest. Start over if the issue persists.
4. Is the dialog outside the shadow DOM while referenced id is inside the shadow DOM (or vice versa)
   - If **Yes** – Make sure both the dialog and an element referenced in aria-labelledby are in the same DOM, or use aria-label instead. Retest. Start over if the issue persists.
   - If **No** – Go to the [Tricky cases](#tricky-cases) section
## Tricky cases
1. Is the dialog's content loaded with a delay (Check for progress bar, but also observer DOM changes, consider debugging and breakpoints). Is aria-label/aria-labelledby content populated with a delay **OR** element referenced inside aria-labelledby is populated with a delay?
   - If **Yes** – If the issue is related to aria-labelledby, consider replacing it with aria-label, or populate aria-label/aria-labelledby without a delay. Retest. Start over if the issue persists.
   - If **No** – Continue
2. Is any dialog's ancestor element a [widget](https://www.w3.org/TR/wai-aria-1.2/#widget_roles)?
   - If **Yes** – change the DOM structure, a dialog cannot have widget ancestor. There are likely more DOM semantics/nesting related issues. Retest. Start over if the issue persists.
   - If **No** – troubleshooting steps need at least one more step, or you missed something. Stop.
