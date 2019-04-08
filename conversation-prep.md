
# Conversation Prep
This document is intended to help prepare an Ember expert for a conversation about accessibility and assumes no prior knowledge. 

This prep document is divided into three main sections: 

1. Screen Reader Basics
2. A11y in Ember
3. Reference Materials & Additional Resources

## Screen Reader Basics 

The intent of this section is to provide the bare minimum information required to think about this problem space. 

How a screen reader works
- Read [“Semantics to Screen Readers”](https://alistapart.com/article/semantics-to-screen-readers) by Melanie Richards
- Watch [“How A Screen Reader User Accesses The Web”](https://www.smashingmagazine.com/2019/02/accessibility-webinar/)  by Léonie Watson 
- Be aware that there are pre-existing keyboard shortcuts- https://dequeuniversity.com/screenreaders/ 


## A11y in Ember 

This section has three sub-sections: 

1. Routing 
2. Modals
3. Thinking about a roadmap 

### Routing (in Ember)
(presentation deck & thinking about solutions)

Watch a short video that demonstrates the issue: https://youtu.be/Jr-de-YV4X0

Other Existing Solutions
We should review these approaches to see if they are feasible:

- ember-a11y
- ember-self-focused
- reach-router

### Modals (in Ember)

Problem Statement and Research Document for Discussion: 
“Supporting Accessible Modals in Ember”  

Additional Reading/References:
- Read [“Making Modal Windows Better for Everyone”](https://www.scottohara.me/blog/2016/09/07/revised-modal-window.html) by Scott O’Hara
- https://www.w3.org/TR/wai-aria-practices/examples/dialog-modal/dialog.html
- https://github.com/gdkraus/accessible-modal-dialog/blob/master/modal-window.js
- Inert Polyfill https://github.com/WICG/inert

### Research for an Accessibility Roadmap in Ember- Draft
What could a roadmap or book of work look like for A11y in Ember?
- https://github.com/MelSumner/ember-a11y-roadmap 

## Reference Materials & Additional Resources

This section has five sub-sections: 

- WAI-Aria Spec
- Existing Developer Guides
- The Future of A11y
- The Current State of A11y
- existing leadership in the accessibility space.

### WAI-ARIA Specification Reference Materials
These are for your reference, because you will want to be able to reference these. 

- W3C Web Accessibility Initiative - https://www.w3.org/WAI/ ←-this is an accessible website
  - Standards and Guidelines - https://www.w3.org/WAI/standards-guidelines/
  - User Agent Accessibility Guidelines- https://www.w3.org/WAI/standards-guidelines/uaag/
- Web Content Accessibility Guidelines (WCAG) 2.0 - https://www.w3.org/TR/WCAG20/
- How to meet WCAG 2.0 - https://www.w3.org/WAI/WCAG21/quickref/

### Existing Developer Guides
- https://www.accessibility-developer-guide.com/
- https://a11yproject.com/about
- https://www.24a11y.com/
- https://developers.google.com/web/fundamentals/accessibility/
- http://heydonworks.com/practical_aria_examples/

### The Future of Accessibility
This is an opportunity to get involved in the next thing- we definitely need to pay attention to this, because they are planning on providing guidelines/standards/recommendations to frameworks. 

- The Silver Task Force- https://www.w3.org/WAI/GL/task-forces/silver/

### The Current State of Accessibility
This is the current, and seemingly persistent mood of the digital accessibility space. I think these are important to be aware of so we can thoughtfully fix this issue - the foundation of JS frameworks is a mindset that has ignored a11y, leading to a lot of bad feelings in the web community at large.  

- “Single Page Apps Routers are Broken” by Rob Deluca - https://medium.com/@robdel12/single-page-apps-routers-are-broken-255daa310cf
- The WebAIM Million- https://webaim.org/projects/million/ ←this is the data we can use
- “Fighting Uphill” by Eric Bailey - https://ericwbailey.design/writing/2019-03-05-fighting-uphill.html
- “The Web We Broke” by Ethan Marcotte https://ethanmarcotte.com/wrote/the-web-we-broke/
- “Accessibility is not a React Problem” - https://www.netlify.com/blog/2019/02/25/accessibility-is-not-a-react-problem/
- “Building Better Accessibility Primitives” by Rob Dodson https://robdodson.me/building-better-accessibility-primitives/

### Existing leadership in the digital accessibility space
These are the people of whose work I recommend being minimally aware:

- Léonie Watson - https://tink.uk/
- Steve Faulkner- https://twitter.com/stevefaulkner
- Jamie Teh - Mozilla/Firefox (formerly NVDA)
- Melanie Richards, Microsoft 
- Rob Dodson, Google (https://robdodson.me/) 
- Marcie Sutton, A11y speaker, React - https://marcysutton.com/
- Derek Featherstone, prominent speaker on Inclusive Design - https://aneventapart.com/speakers/derek-featherstone
