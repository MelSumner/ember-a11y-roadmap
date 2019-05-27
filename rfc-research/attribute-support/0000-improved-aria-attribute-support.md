This issue: https://github.com/emberjs/ember.js/issues/17692#issuecomment-469378810
Led to the creation of this RFC issue: https://github.com/emberjs/rfcs/issues/476
This RFC attempts to address the issues laid out in that RFC.

===============================================================================

- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Relevant Team(s): (fill this in with the [team(s)](README.md#relevant-teams) to which this RFC applies)
- RFC PR: (after opening the RFC PR, update this with a link to it and update the file name)
- Tracking: (leave this empty)

# <RFC title>

## Summary

Ember should provide better support for aria attributes as part of the framework-wide effort to provide better developer support for building accessible applications. 

## Motivation

Right now, `aria-*` attributes _that can receive multiple values, **and** for whom the order of those values matter_, are not well-supported in Ember. While [RFC #435](https://github.com/emberjs/rfcs/pull/435) provided support for forwarding element modifiers with "splattributes", it did not provide the necessary support for these `aria` attributes.

## Detailed design

### Improve attribute value merging 

Right now, the `class` attribute is the only attribute that receives an exception to the default attribute merging rules. However, there are five `aria` attributes in the accessibility specification whose value is an ID reference list (meaning, they can have one or more values):

- [aria-controls](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-controls)
- [aria-describedby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-describedby)
- [aria-flowto](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-flowto) 
- [aria-labelledby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-labelledby) 
- [aria-owns](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-owns) 

Since this order can matter, the author should be able to specify that order themselves - the same way they can currently specify the values for the `class` attribute.

Think about it in this way: 

(The cat) (ran) (to me)

This is a sentence in three parts. The three parts of this sentence matter- If I said "Ran the cat to me", that might not make a lot of sense (unless I was Yoda). 

We can also think about this in the context of why the order of the values of the `class` attribute matter on an HTML element. 

## How we teach this

There are some `aria` attributes that can receive multiple values. Since this order can matter (the same way the order of `class` attribute values can matter for CSS), Ember will respect the order that you define the values for these attributes. 

## Drawbacks

- we are adding more exceptions to the rule. Usually something we try to avoid. 

## Alternatives

- implement exceptions for only the two most common ones- `aria-labelledby` and `aria-describedby`
- re-write the entire feature to give more granular control

## Unresolved questions

TBD
