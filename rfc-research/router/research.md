# Accessible Routing in Ember - Research

Watch a short video that demonstrates the issue: https://youtu.be/Jr-de-YV4X0

## Summary
The goal is to figure out how to make Ember's router more accessible and screen-reader friendly. When a route transition occurs, _something_ should occur that tells the screen-reader that this transition has occurred. 

Focus should then move to the top left of the page ~, or, as an improvement, to the outermost outlet for that route~ . 

For the purpose of this initial research, we do not care what else wants the focus after that. We only care about triggering that initial focus and placing that focus there so screen-readers are aware. There are reasons for this, but we won't explore those in the summary. 

We're choosing to evaluate and initially try to solve this issue using Firefox and NVDA because both are open source. Theoretically, if we can figure out how to make this work by better understanding NVDA and Firefox, it should also fall into place for other browser and screen-reader combinations. 

This first step is a tightly-scoped endeavor by design. 

## Background Info

### Browser/Screen-Reader combinations

These are the common browser/screen-reader combinations: 
- Internet Explorer & JAWS
- Edge & Narrator
- Firefox & NVDA
- Safari & Voice Over
- Chrome & Chrome Vox

## Research - NVDA


For this bit, I've dug into NVDA's source code [available on Github](https://github.com/nvaccess/nvda). 

### Events in NVDA
From the docs: 

When NVDA detects particular toolkit, API or Operating System events, it abstracts these and fires its own internal events on plugins and NVDA Objects.

Although most events are related to a specific NVDA Object (e.g. name change, gain focus, state change, etc.), these events can be handled at various levels.
When an event is handled, it is stopped from going further down the chain.
However, code inside the event can choose to propagate it further if needed.

The order of levels through which the event passes until an event method is found is:
- Loaded Global Plugins
- The App Module associated with the NVDA Object on which the event was fired
- The Tree Interceptor (if any) associated with the NVDAObject on which the event was fired
- the NVDAObject itself.

Events are Python instance methods, with a name starting with "event_" followed by the actual name of the event (e.g. gainFocus).

These event methods take slightly different arguments depending at what level they are defined.

If an event for an NVDA Object is defined on an NVDA Object itself, the method only takes one mandatory argument which is the 'self' argument; i.e. the NVDA Object instance).
Some events may take extra arguments, though this is quite rare.

If an event for an NVDA Object is defined on a Global Plugin, App Module or Tree Interceptor, the event takes the following arguments:
- self: the instance of the Global Plugin, App Module or Tree Interceptor
- obj: the NVDA Object on which the event was fired
- nextHandler: a function that when called will propagate the event further down the chain.


Some common NVDA Object events are:
- foreground: this NVDA Object has become the new foreground object; i.e. active top-level object
- gainFocus
- focusEntered: Focus has moved inside this object; i.e. it is an ancestor of the focus object
- loseFocus
- nameChange
- valueChange
- stateChange
- caret: when the caret (insertion point) within this NVDA Object moves
- locationChange: physical screen location changes

### Firefox & NVDA

The apps that want to be compatible with NVDA all have a .py file with specific classes for those platforms. The Firefox file has one class. 

```
class AppModule(appModuleHandler.AppModule):

	def event_stateChange(self, obj, nextHandler):
		if obj.role == controlTypes.ROLE_DOCUMENT and controlTypes.STATE_BUSY in obj.states and winUser.isWindowVisible(obj.windowHandle) and obj.isInForeground:
			statusBar = api.getStatusBar()
			if statusBar:
				statusText = api.getStatusBarText(statusBar)
				speech.cancelSpeech()
				speech.speakMessage(controlTypes.stateLabels[controlTypes.STATE_BUSY])
				speech.speakMessage(statusText)
				return
		nextHandler()

	event_gainFocus = event_stateChange
```

## Research - Pre-existing solutions

Let's look at how some other libraries or Ember addons manage focus in routing, because there might be ideas here that we want to try to use or, conversely, avoid: 

- [Reach Router](https://github.com/reach/router)
- [ember-a11y](https://github.com/ember-a11y/ember-a11y)
- [ember-self-focused](https://github.com/linkedin/self-focused/tree/master/packages/ember-self-focused)
- [a11y-announcer](https://github.com/ember-a11y/a11y-announcer)

## Research Questions

While most solutions seem to merely manage focus by tapping into the (render cycle?) - mostly seems like brute force- I wonder if we could create a solution that bridges the gap between the event that NVDA uses for gaining/setting focus, and how the history API is used in Ember to navigate in/around an app. (The history API was written after assistive technology was created.) 

- If history.pushState or history.replaceState happens, could we set the application outlet as the current (focusAncestor?) ?
- add role of document to outlet? (but this shouldn't matter, theoretically)
- add a new role in controlTypes.py that indicates SPA? this would require coordination with NVDA devs



