# ember-a11y-roadmap
A Potential Roadmap for all things a11y in ember.js. 

First, if you are not familiar with digital accessibility, please reference the [conversation prep document](https://github.com/MelSumner/ember-a11y-roadmap/blob/master/conversation-prep.md) first. **You will likely be ill-equipped to think about the problem space without some introduction to the topic.** 

If you wish to contribute to this repository, PRs are welcome.

## Low-effort changes
- Add default language attribute on the `<html>` element
- Release an official framework statement regarding A11y in Ember.js
- Publishing a "roadmap" or "intent to improve" list (along with an invitation to contribute)

## Things we should improve 
- Add support for page titles (should be unique per page)
- the way the router works (or doesn't) with screen readers
- improved support for aria-* attributes (including splattributes)
- focus management
- keyboard navigation
- semantic test helpers (improves code in general but could specifically be used to better test for accessibility conformance)
- A11y in the guides
- component patterns for accessible components
- linting
- ember language server support

## Innovation Opportunities
Right now, only about 30% of accessibility issues can be automatically tested. We have the opportunity to improve that through innovative tooling. 
- CLI tool for http://adrianroselli.com/2019/04/reading-order-bookmarklet.html

## RFCs 

### Existing
- [accessible routing in Ember.js](https://github.com/emberjs/rfcs/pull/433)
- [semantic test helpers](https://github.com/emberjs/rfcs/pull/327)

### Research/write
- vocalizing support for assistive technology (screen readers, specifically) in the same way we list browser support
- dialogs/modals (parent window inert, focus management) [[RFC Research]](dialogs/modals.md)
- keyboard nav
- focus management

## Documentation
- [guides & developer education](documentation/guides.md)
- a11y for the [emberjs.com guides](https://guides.emberjs.com/release/reference/accessibility-guide/) 
- Add a11y check/section to RFC process
- update ember-a11y website
 - add best practices for ember components
 - give helpful information for ember addons
- improved [developer experience](linting-and-testing/approach.md) 

## Addons
ui addon with a11y-first approach

- https://github.com/MelSumner/e-a11y-modal
