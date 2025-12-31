# Button

## What is a button?
1. Button is a control, which is presented to assistive technologies with the button role.
2. A user can interact with a button in a predicatable way (interaction is the same as for all other buttons)

## Enabled button checklist
- [Button has the correct role](button-role.md)
- [Button has a name](button-name.md)
- Button's label and name describe its purpose
- Button's label is included in its name
- Button's name doesn't include role
- Button's name doesn't include operating instructions
- Button's description doesn't include standard keyboard operating instructions
- Button which looks the same and performs the same action should have a consistent name
- Button can be reached with the Tab key
- Button has visible focus indicator
- Button can be activated with Enter ***and*** Space keys
- Button is not used to navigate between URLs
- [Button shouldn't contain any redundant attributes](button-redundant-attributes.md)

## Before you start implementation
While it's possible to create a [custom button](native-button-vs-custom-button.md) which meet all the criteria above, consider using the `<button>` tag. It's a huge time saver.
