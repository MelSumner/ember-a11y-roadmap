# ember-a11y-roadmap
A Potential Roadmap for all things a11y in ember.js. 

First, if you are not familiar with digital accessibility, please reference the [conversation prep document](https://github.com/MelSumner/ember-a11y-roadmap/blob/master/conversation-prep.md) first. **You will likely be ill-equipped to think about the problem space without some introduction to the topic.** 

If you wish to contribute to this repository, PRs are welcome.

## List of things we could improve 
- the way routing works with screen readers
- focus management
- modals/popups/alerts
- keyboard navigation
- semantic test helpers (improves code in general but could specifically be used to better test for accessibility conformance)


## RFCs that exist
- [accessible routing in Ember.js](https://github.com/emberjs/rfcs/pull/433)
- [semantic test helpers](https://github.com/emberjs/rfcs/pull/327)

## RFC ideas to research/write
- vocalizing support for assistive technology (screen readers, specifically) in the same way we list browser support
- modals (parent window inert, focus management) [[RFC Research]](https://github.com/MelSumner/ember-a11y-roadmap/blob/master/rfc-research/modals.md)
- keyboard nav
- focus management

## Documentation
- [guides & developer education](guides.md)
- a11y for the [emberjs.com guides](https://guides.emberjs.com/release/reference/accessibility-guide/) 
- Add a11y check/section to RFC process
- update ember-a11y website
 - add best practices for ember components
 - give helpful information for ember addons

## Addons and Support
- better [linting](linting.md) 
- ui addon with a11y-first approach
