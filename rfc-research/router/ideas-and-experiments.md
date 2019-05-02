# Ideas and Experiments

## Ideas 
- review pushState
- try some post render experiments to see what happens.
- Could we make the boundary of the outlet a little more exposed so we can use that? 
  - Could we use it even if it's not a little more exposed? 
  - What would it look like to "officially" focus on the first item in the outlet when the route transitions? 

## Experiments and Results
Repo for Ember app used: https://github.com/MelSumner/three-nine-zero

### Looking at pushState
We should figure out what(if anything) went wrong with `pushState`- thinking back, we thought it was going to be fine for a11y. Was it implemented poorly, or did the design not deliver what we thought it would? Using https://codesandbox.io/s/github/rwjblue/screenreader-testing, we can do some experimentation ([GitHub repo here](https://github.com/rwjblue/screenreader-testing)). 

### Static Rendering
Installing Fastboot AND turning off JavaScript in the browser did produce the desired results- the page read out as expected with the screenreader.  

### Check the scheduling
- Does it have anything to do with scheduling?
- No. We confirmed this by stepping through with the debugger and the transition is definitely on the same stack with no async calls. Nothing was scheduled. 

### Setting "container" focus
- Body element focus: Setting focus on the `<body>` element DID move the focus, but it didn't read out the new page content as we desired. 
- first div in the body: this also moved the focus but nothing was read out in the screen reader. 
- Setting focus on an element that we know changed in the routes: **This worked.** The screen reader read out the new content. In this case, we focused on the h1 for each page. However this only worked when we wrapped the code to set focus in a setTimeout function.

This Worked (in application.js): 
```js
import Route from '@ember/routing/route';
import { inject as service } from '@ember/service';

export default Route.extend({
  router: service('router'),
  init() {
    this._super(...arguments);
    this.router.on('routeDidChange', transition => {
      if (document.activeElement) {
        document.activeElement.blur();
      }

      if (transition.to !== null) {
        setTimeout(function() {
          document.body.querySelector('div').setAttribute("tabindex", "-1");
          document.body.querySelector('div').focus();
        }, 0);
        
      }
    });
  }
});
```
This did not work: 
```js
import Route from '@ember/routing/route';
import { inject as service } from '@ember/service';

export default Route.extend({
  router: service('router'),
  init() {
    this._super(...arguments);
    this.router.on('routeDidChange', transition => {
      if (document.activeElement) {
        document.activeElement.blur();
      }

      if (transition.to !== null) {
          document.body.querySelector('div').setAttribute("tabindex", "-1");
          document.body.querySelector('div').focus();        
      }
    });
  }
});
```

### Adding route navigation message
> The first thing you learn to do as a screen-reader user, is make the screen reader stop talking. 

#### The idea 
what if we can add a message to the screen reader user, letting them know that the page (route) transition has occurred successfully, and they can now navigate as they wish? 

#### Implementation
In our [test app](https://github.com/MelSumner/three-nine-zero), edits were made to four files (code below):

- templates/application.hbs, 
- controllers/application.js, 
- routes/application.js
- styles/app.css

**Note: This is not a polished approach- the implementation forces focus and shows that content on focus for the purpose of evaluating this prototype. Evaluators should imagine how this could work in its final state, should we choose to proceed with this option.**

templates/application.hbs:

```hbs
<div tabindex="-1" class="ember-sr-only sr-only-focusable" id="nav-message">Navigation to {{this.currentURL}} is complete. You may now navigate as you wish.</div>
```

controller/application.js: 

```js
import Controller from '@ember/controller';
import { computed } from '@ember/object';
import { inject as service } from '@ember/service';

export default Controller.extend({
  router: service(),
  currentURL: computed('router.currentURL', function() {
    return this.router.currentURL;
  })
});
```

routes/application.js:

```js
import Route from '@ember/routing/route';
import { inject as service } from '@ember/service';

export default Route.extend({
  router: service('router'),
  init() {
    this._super(...arguments);
    this.router.on('routeDidChange', transition => {

      if (document.activeElement) {
        document.activeElement.blur();
      }

      if (transition.to !== null) {
        setTimeout(function() {
          document.body.querySelector('#nav-message').setAttribute("tabindex", "-1");
          document.body.querySelector('#nav-message').focus();
        }, 0);        
      }
    });
  }
});
```

styles/app.css

```css
/*
  Only display content to screen readers
  See: https://a11yproject.com/posts/how-to-hide-content/
  See: https://hugogiraudel.com/2016/10/13/css-hide-and-seek/
*/

.ember-sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/*
  Use in conjunction with .sr-only to only display content when it's focused.
  Useful for "Skip to main content" links; see https://www.w3.org/TR/2013/NOTE-WCAG20-TECHS-20130905/G1
*/
.ember-sr-only.sr-only-focusable:active,
.ember-sr-only.sr-only-focusable:focus {
    position: static;
    width: auto;
    height: auto;
    overflow: visible;
    clip: auto;
    white-space: normal;
}
```



### Questions to answer: 

Does the screen reader have some sort of dom cache, where if we pass it the same element with new content, it doesn't read it out because it thinks it's the same element/content? 

If this is true, then the next thing to try would be to see if we could find a way to set the focus on the first element in the newly rendered outlet.
