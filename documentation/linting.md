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


## Practical Approach

This is a bit of an update from the initial theorized approach. After some discussion, we believe that it will be useful to keep using ember-a11y-testing in addition to ember-template-lint, especially as ember-a11y-testing has improved their performance and should resolve the performance concerns. 

### Areas of focus

In order to ensure that all of our community testing covers all facets of accessibility, we will use this strategy: 

- use ember-a11y-testing for WCAG criteria (since its already covered in axe-core)
- use ember-template-lint to test for common success and failure techniques as listed in https://www.w3.org/TR/WCAG20-TECHS/. 
- where impractical for testing, we will work to include it in Ember Language Server 

#### ember-template-lint
Repo: https://github.com/ember-template-lint/ember-template-lint 

- Issues should be formatted like this: https://github.com/ember-template-lint/ember-template-lint/issues/626 
- PRs to address these issues must link to the specification, and not rules in other linting applications 
- Mel will review each issue and assign to Rob for second review/merging
- Since each new rule is considered a breaking change for semVer, we will batch a11y rules at reasonable intervals

#### ember-a11y-testing
Repo: https://github.com/ember-a11y/ember-a11y-testing

- we will add Dependabot or Renovate in order to ensure that this addon is kept up-to-date


