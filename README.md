# ember-a11y-roadmap
A Potential Roadmap for all things a11y in ember.js. 

First, if you are not familiar with digital accessibility, please reference the [conversation prep document](https://github.com/MelSumner/ember-a11y-roadmap/blob/master/conversation-prep.md) first. **You will likely be ill-equipped to think about the problem space without some introduction to the topic.** 

If you wish to contribute to this repository, PRs are welcome.

## Things we should improve 
- the way routing works with screen readers
- focus management
- modals/popups/alerts
- keyboard navigation
- semantic test helpers (improves code in general but could specifically be used to better test for accessibility conformance)
- linting
- ember language server support
- improved support for aria-* attributes

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
