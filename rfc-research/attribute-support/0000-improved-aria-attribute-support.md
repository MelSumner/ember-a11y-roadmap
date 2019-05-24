- Start Date: (fill me in with today's date, YYYY-MM-DD)
- Relevant Team(s): (fill this in with the [team(s)](README.md#relevant-teams) to which this RFC applies)
- RFC PR: (after opening the RFC PR, update this with a link to it and update the file name)
- Tracking: (leave this empty)

# <RFC title>

## Summary

Ember should provide better support for aria attributes as part of the framework-wide effort to provide better developer support for building accessible applications. 

## Motivation

Right now, `aria-*` attributes are not well-supported in Ember. While [RFC #435](https://github.com/emberjs/rfcs/pull/435) provided support for forwarding element modifiers with "splattributes", it did not provide the necessary support for aria-attributes- especially the ones that accept multiple attribute values and for whom the order matters. 

## Detailed design

### Improve attribute value merging 

Right now, the `class` attribute is the only attribute that receives an exception to the default attribute merging rules. However, there are five `aria` attributes in the accessibility specification whose value is an ID reference list (meaning, they can have one or more values):

- [aria-controls](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-controls)
- [aria-describedby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-describedby)
- [aria-flowto](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-flowto) 
- [aria-labelledby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-labelledby) 
- [aria-owns](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-owns) 

Since this order can matter, the author should be able to specify that order themselves - the same way they can currently specify the values for the `class` attribute.

An Example (note the `aria-describedby` attribute on the `input` element): 

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

## How we teach this

There are some `aria` attributes that can receive multiple values. Since this order can matter (the same way the order of `class` attribute values can matter for CSS), Ember will respect the order that you define the values for these attributes. 

## Drawbacks

TBD

## Alternatives

I have not yet identified any alternative methods to implementing this RFC.

## Unresolved questions

TBD
