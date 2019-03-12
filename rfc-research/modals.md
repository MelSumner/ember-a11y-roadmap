# Supporting Accessible Modals in Ember.js
While we may wish we lived in a world where modals did not exist, they do; despite our best effort, sometimes they must be used. We will review the ways modals should work, some common pain points for developers and users with assistive technology, and list some ways that we could potentially improve the developer ergonomics in this area. 

## Intro to some terminology  
There are two types of modals: 
- [Dialog(Modal)](https://www.w3.org/TR/wai-aria-practices/#dialog_modal)
- [Alert and Message Dialogs](https://www.w3.org/TR/wai-aria-practices/#alertdialog)

A **dialog modal** will have more text and interactive elements than an **alert modal**. For example, a dialog modal could ask the user to fill out a form. An alert or message dialog is for situations where you need to bring the user's attention immediately to an urgent message. For example, deleting a record could show an alert dialog that says "You're about to delete this record. Are you sure?" 

### Keyboard Navigation
There are three keyboard navigation pieces to modals. When a dialog opens, focus moves to an element inside the dialog. After that, three keyboard navigation (combinations?) must work:  
- TAB
  - Moves focus to the next tabbable element inside the dialog.
  - If focus is on the last tabbable element inside the dialog, moves focus to the first tabbable element inside the dialog.
- SHIFT + TAB:
  - Moves focus to the previous tabbable element inside the dialog.
  - If focus is on the first tabbable element inside the dialog, moves focus to the last tabbable element inside the dialog.
- ESC
  - Closes the dialog.

## Common failures
These are the areas that developers often fail to get modals correct. Incorrect behavior in any of these areas makes modals a frustrating, if not unusable, experience for users with assistive technology. 

- modals that don't limit interaction to the modal itself
- where the focus goes when the modal opens
- where the focus goes when the modal closes
- forgetting to make sure the ESC key closes the modal window
- modal content gets inserted dynamically in the wrong places (i.e., just inside of the body tag).
- missing aria-* and role attributes

## A possible solution
If we were going to make this work, how _could_ we do it? 

If we could solve anything in Ember natively, narrowing scope to the most common issue would be a reasonable approach. If possible, Ember could ensure that if a modal is open, the parent window is toggled to an inert state (often referred to as a "focus trap").

### The Inert Attribute

There is a polyfill available for the `inert` HTML attribute (see [inert polyfill](https://github.com/WICG/inert)). Since Ember has already demonstrated a willingness to use polyfills when necessary, it seems reasonable that a polyfill that provides a much needed accessibility feature to the framework would be acceptable. 

Try it out for yourself: https://wicg.github.io/inert/demo/ 

This is how you can do this in React[\*](https://github.com/WICG/inert/issues/58): 
- Use the node's ref to set the inert attribute
```js
return <div ref={node => node && node.setAttribute('inert', '')} />
```
- Or, conditionally: 
 ```js
 <div
  ref={node => node && (shouldBeInert ?
    node.setAttribute('inert', '') : node.removeAttribute('inert')
  )}
/>
```
## Why we should do this
Implementing `inert` as a low-level primitive in Ember would not only provide a out-of-the-box way to support modals, but also make it easier to accessibly implement infinite scrolling UIs (specifically, ones that re-uses or pre-renders nodes). 

This could be an optional feature that the user opts into, the same way they opt into removing the application template wrapper. 

## Alternatives
- have an officially supported addon - ember-a11y-modal
- screen for common failures through linting 