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

Right now, the position of `...attributes` indicates whether or not an attribute value can be overridden:

```hbs
<div data-foo="inner" ...attributes></div>
<div ...attributes data-foo="inner"></div>
```
With this invocation:

```hbs
<Foo data-foo="outer" />
```

We expect the location of `...attributes` to affect the final result:

```hbs
<div data-foo="outer"></div>
<div data-foo="inner"></div>
```

That is, *unless* it is the `class` attribute. With the `class` attribute, placement of `...attributes` indicates the order in which the values should be merged.

If we wrote this: 

```hbs
<div data-foo="inner" class="red" ...attributes>
```

With this invocation:

```hbs
<Foo class="blue" />
```

The `...attribute` placement will effect the way the (CSS) classes are ordered: 

```hbs
<div data-foo="inner" class="red blue">
```

Now, if we had written this:
```hbs
<div data-foo="inner" ...attributes class="red">
```

With this invocation:

```hbs
<Foo class="blue" />
```

The `...attribute` placement BEFORE the `class` attribute will cause the classes to be ordered differently:

```hbs
<div data-foo="inner" class="blue red">
```

For the `aria` attributes in this RFC, the expectation is that they would work the same way as the `class` attribute. 




## How we teach this

There are some `aria` attributes that can receive multiple values. Since this order can matter (the same way the order of `class` attribute values can matter for CSS), Ember will respect the order that you define the values for these attributes. 

## Drawbacks

- we are adding more exceptions to the rule. 

## Alternatives

- implement exceptions for only the two most common ones- `aria-labelledby` and `aria-describedby`
- re-write the entire feature to give more granular control
- update the guides to inform users that for these `aria` attributes, they must make it so they can always be overridden, and ensure that developers understand that multiple values can be provided **and** that the order matters. 

## Unresolved questions

- Are there other attributes that both accept multiple values and also for who that value order matters? While this RFC covers all of the ones listed in the ARIA spec
