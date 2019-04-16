# Ideas and Experiments

## Ideas 

### Looking at pushState
We should figure out what went wrong with pushState- thinking back, we thought it was going to be fine for a11y. Was it implemented poorly, or did the design not deliver what we thought it would?

### Post Render
maybe it needs to be done post render?

### Thinking about focus and security
another issue is, focus setting needs to trace back to the click for security- it needs to be tied to the user action. 
There maybe something we are doing with scheduling that is affecting it...Click has an elevated context, security wise. It can schedule things that inherit this - but if we do things that queue and schedule, we could mess that context up. But that would break things like people opening a popup, etc.

## Experiments and Results

### Check the scheduling
- Does it have anything to do with scheduling?
- No. We confirmed this by stepping through with the debugger and the transition is definitely on the same stack with no async calls. Nothing was scheduled. 

### Setting "container" focus
- Setting focus on body?
- Setting focus on body DID fix the focus issue, but it didn't read out the new page content as we desired. 

We tried: 
- setting focus on the body
- setting focus on the first div in the body 

```
  document.body.querySelector('div').setAttribute("tabindex", "-1");
  document.body.querySelector('div').focus();
```

- Q. Setting focus on an element that we know changed in the routes?
- A. This worked. It read out the new content. 

### Next question to answer: 

Does the screen reader have some sort of dom cache, where if we pass it the same element with new content, it doesn't read it out because it thinks it's the same element/content? 

If this is true, then the next thing to try would be to see if we could find a way to set the focus on the first element in the newly rendered outlet.
