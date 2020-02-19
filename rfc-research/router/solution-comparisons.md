# Solution Comparisons

This document will review the current solutions and provide additional reading materials. Have additional information to add? PRs are welcome.

## Current Landscape

### Solutions

- React - [Reach router](https://github.com/reach/router) - used by [Gatsby](https://www.gatsbyjs.org/docs/making-your-site-accessible/#accessible-routing)
- Angular - docs include instructions for managing focus for routing: https://angular.io/guide/accessibility#routing-and-focus-management
- Ember:
  - Focus management addons: [ember-a11y](https://github.com/ember-a11y/ember-a11y) & [ember-self-focused](https://github.com/linkedin/self-focused/tree/master/packages/ember-self-focused) 
  - Route announcement addon: [a11y-announcer](https://github.com/ember-a11y/a11y-announcer)
  - Route announcement + focus management: [ember-a11y-refocus](https://github.com/MelSumner/ember-a11y-refocus) - Demo site (with message visible for demonstration purposes)- https://navigator-message-test-app.netlify.com/

### Documentation

- [Angular Guides: Accessibility](https://angular.io/guide/accessibility)
- [Ember Guides: Accessibility](https://guides.emberjs.com/release/accessibility/)
- [React Documentation: Accessibility](https://reactjs.org/docs/accessibility.html)
- Vue doesn't have accessibility in their documentation, but a side project has been started- https://vue-a11y.com/


## Existing Research

In addition to the [other materials](https://github.com/MelSumner/ember-a11y-roadmap/blob/master/rfc-research/router/research.md) in this repository, here are links to some other research that has already been done: 

- [What we learned from user testing of accessible client-side routing techniques with Fable Tech Labs](https://www.gatsbyjs.org/blog/2019-07-11-user-testing-accessible-client-routing/)
- [Single Page Apps routers are broken](https://medium.com/@robdel12/single-page-apps-routers-are-broken-255daa310cf)
