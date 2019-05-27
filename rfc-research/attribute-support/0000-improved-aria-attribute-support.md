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

Right now, `aria-*` attributes that can receive multiple values, **and** for whom the order of those values matter are not well-supported in Ember. While [RFC #435](https://github.com/emberjs/rfcs/pull/435) provided support for forwarding element modifiers with "splattributes", it did not provide the necessary support for these `aria` attributes.

## Detailed design

### Improve attribute value merging 

Right now, the `class` attribute is the only attribute that receives an exception to the default attribute merging rules. However, there are five `aria` attributes in the accessibility specification whose value is an ID reference list (meaning, they can have one or more values). We could also break it down further: Order **definitely** matters and the use case is common, and order **could** matter but use case is less common. 

Used often: 
- [aria-describedby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-describedby)
- [aria-labelledby](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-labelledby) 

Used less often:
- [aria-flowto](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-flowto) 
- [aria-controls](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-controls)
- [aria-owns](https://www.w3.org/WAI/PF/aria/states_and_properties#aria-owns) 

Since this order can matter, the author should be able to specify that order themselves - the same way they can currently specify the values for the `class` attribute.

This is a sentence in three parts:

(The cat) (ran) (to me)

The order of the three parts of this sentence matter- If I said "Ran the cat to me", that might not make a lot of sense. We can also think about this in the context of why the order of the values of the `class` attribute matter on an HTML element. 

Right now, the position of `...attributes` indicates whether or not an attribute value can be overridden. This is, with the exception of class. The position of the `class` attribute indicates the order of the values. 

### Scenario 1

Here's what happens if I create a `my-input` component that uses the `aria-describedby` attribute with multiple values. In this contrived example, I'm setting up a input where the user can set a password. I'll use help text to give the user additional informatiuon about what the password needs to include. However, developer who is using my component to implement the requirements for their product wants to add additional help text. 

Component:

```hbs
<label for="input" class="form-label" ...attributes>{{@input-label}}</label>
<input type="text" id="input" ...attributes aria-describedby="text-help-0"  />
<span class="text-help" id="text-help-0">
  Password Requirements: Must contain at least one letter and one number.
</span>
```

Invocation:

```hbs
  <MyInput @input-label="Password" aria-describedby="text-help-0 text-help-1" />
  <span class="text-help" id="text-help-1">Must also include a special character.</span>
```

Result: 
We expect the location of `...attributes` to affect the final result- and it does. `aria-describedby` only has one value, `text-help-0`: 

```hbs
  <input id="input" aria-describedby="text-help-0" type="text">
```

The other isn't associated with the input. This means that the sighted user will see all of the help text. The user with a screen reader will only receive part of the instructions, leaving them unable to complete the task. 

### Scenario 2
However, if we moved the position of the `...attributes` in our component: 

```hbs
<input type="text" id="input" aria-describedby="text-help-0"  ...attributes />
```

If the developer invoked this component the same way they would for the `class` attribute (because they want to add additional ones, not replace existing ones):

```hbs
  <MyInput @input-label="Password" aria-describedby="text-help-1" />
  <span class="text-help" id="text-help-1">Must also include a special character.</span>
```

We will get this result: 
```hbs
  <input id="input" aria-describedby="text-help-1" type="text">
```

The `...attribute` placement has made it so the `aria-describedby` value has been completely replaced, not appended. This means, again,  that the sighted user will see all of the help text but the user with a screen reader will only receive part of the instructions, leaving them unable to complete the task. 

### Scenario 3

The workaround is to know what the `aria-describedby` value is already declared in the component, and make sure that both are declared when the component is invoked:

Component: 
```hbs
<label for="input" class="form-label">{{@input-label}}</label>
<input type="text" id="input" aria-describedby="text-help-0" ...attributes />
<span class="text-help" id="text-help-0">
  Password Requirements: Must contain at least one letter and one number.
</span>
```

Invocation: 
```hbs
  <MyInput @input-label="Password" aria-describedby="text-help-0 text-help-1" />
  <span class="text-help" id="text-help-1">Must also include a special character.</span>
```

Result: 
```hbs
  <input id="input" aria-describedby="text-help-0 text-help-1" type="text">
```

However, For the `aria` attributes in this RFC, the expectation is that they would work the same way as the `class` attribute. The descrepancy will cause developer confusion. 


## How we teach this

We can add a section to the guides: 
There are some `aria` attributes that can receive multiple values. Since this order can matter (the same way the order of `class` attribute values can matter for CSS), Ember will respect the order that you define the values for these attributes. 

## Drawbacks

- we are adding more exceptions to the rule. 

## Alternatives

- implement exceptions for only the two most common ones- `aria-labelledby` and `aria-describedby`
- re-write the entire feature to give more granular control
- update the guides to include scenario 3 as just the way it works. [PR 822](https://github.com/ember-learn/guides-source/pull/822)

## Unresolved questions

- Are there other attributes that both accept multiple values and also for who that value order matters? While this RFC covers all of the ones listed in the ARIA spec
