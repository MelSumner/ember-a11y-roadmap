# Linting

To help provide developers with a better well-lit path to successfully build accessible Ember applications, we intend to take a multi-faceted approach. One of the facets of this approach is better lint messaging. 

## Improving what exists

We intend to improve the messaging already provided through the [`ember-template-lint`](https://github.com/ember-template-lint/ember-template-lint/) addon. 

### Improving Linting Error messages: 

- compare rules already available through axe-core. 
- compile list of all rules that we can automate for, ensuring that all WCAG criteria are accounted for. 
- consult the list of techniques and failures to evaluate for automation (and account for all of them in some manner). 
- file issues in the `ember-template-lint` repository and include references, samples of conformant and non-conformant code, suggested error message, and references to the WAI-ARIA specification for that conformance criteria (see https://github.com/ember-template-lint/ember-template-lint/issues/626 as an example of a correctly formatted issue)
- The maintainers have agreed to periodically release groups of ember-template-lint rules; the addition of any new rules is a semver breaking change, and there will be a lot of new template lint rules, so it makes sense to do them in batches. 


### Improving Language Servers

For some accessibility criteria, it makes more sense to include them in the ember-language-server instead of a linting addon. For example, checking to make sure every dom element isn't using an incorrect role (or a made up role!) is potentially performance heavy. For things like this, we intend for this to be done through an extension for IDEs. 
