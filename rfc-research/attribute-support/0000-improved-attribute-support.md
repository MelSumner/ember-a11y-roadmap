- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Relevant Team(s): (fill this in with the [team(s)](README.md#relevant-teams) to which this RFC applies)
- RFC PR: (after opening the RFC PR, update this with a link to it and update the file name)
- Tracking: (leave this empty)

# <RFC title>

## Summary

Ember should provide better support for aria attributes as part of the framework-wide effort to provide better developer support for building accessible applications. 

## Motivation

Right now, `aria-*` attributes are not well-supported in Ember. While [RFC #435](https://github.com/emberjs/rfcs/pull/435) provided support for forwarding element modifiers with "splattributes", it did not provide the necessary support for aria-attributes- especially the ones that accept multiple attribute values and for whom the order matters. Additionally, Ember could more sensibly support some `aria-*` attributes to improve the developer experience.  

## Detailed design

### Improve attribute value merging 

Right now, the `class` attribute is the only attribute that receives an exception to the default attribute merging rules. However, there are six `aria` attributes in the accessibility specification whose value is an ID reference list (meaning, they can have one or more values):

- [aria-controls](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-controls)
- [aria-describedby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-describedby)
- [aria-flowto](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-flowto) 
- [aria-labelledby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-labelledby) 
- [aria-owns](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-owns) 

Since this order can matter, the author should be able to provide that order themselves.

Example (rendered): 
```html

<label for="special_instructions">
    Special instructions:
</label>
<input id="special_instructions"
       type="text"
       aria-describedby="special_instructions_desc-1 special_instructions_desc-2"
       class="wide_input">
<div class="help_text" id="special_instructions_desc-1">
  For example, gate code or other information to help the driver find you
</div>
<div class="help_text" id="special_instructions_desc-2">
  More special instructions here (maybe they came from a different place, or this is where the error text will show up).
</div>
```

### Improve attributes 



## How we teach this

> What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing Ember patterns, or as a
wholly new one?

> Would the acceptance of this proposal mean the Ember guides must be
re-organized or altered? Does it change how Ember is taught to new users
at any level?

> How should this feature be introduced and taught to existing Ember
users?

## Drawbacks

> Why should we *not* do this? Please consider the impact on teaching Ember,
on the integration of this feature with other existing and planned features,
on the impact of the API churn on existing apps, etc.

> There are tradeoffs to choosing any path, please attempt to identify them here.

## Alternatives

> What other designs have been considered? What is the impact of not doing this?

> This section could also include prior art, that is, how other frameworks in the same domain have solved this problem.

## Unresolved questions

> Optional, but suggested for first drafts. What parts of the design are still
TBD?
