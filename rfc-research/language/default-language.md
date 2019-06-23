# Default language settings

Summary: Ember applications should not fail accessibility success criteria immediately after creating a new Ember application. Currently, the lack of the `lang` attribute on the `<html>` element in the index.html file causes a failure.  

## Related WCAG success criteria
- [language of the page](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=311%2C312#language-of-page)
- [language of the parts](https://www.w3.org/WAI/WCAG21/quickref/?showtechniques=311%2C312#language-of-parts)

## Existing ecosystem solutions

### addon - ember-intl

App devs can use [ember-intl](https://github.com/ember-intl/ember-intl) to dynamically set the language of the page if they choose to localize their application. This addon changes the value of the `lang` attribute on the `<html>` element. 

### manually set a language value

Apps devs can manually set a language value by editing the index.html file in their applications

### ember-a11y-testing

The ember-a11y-testing solution will inform the application developer that they have failed to meet the relevant WCAG criteria by failing to set a `lang` attribute on the `<html>` element. 

## Assistive Tech
How does assistive technology handle this issue on a practical level?

### NVDA
This is a combo box which allows you to select the language that NVDA's user interface and messages should be shown in. There are many languages, however the default option is "User Default, Windows". This option tells NVDA to use the language that Windows is currently set to.

Please note that NVDA must be restarted when changing the language. When the confirmation dialog appears, select "restart now" or "restart later" if you wish to use the new language now or at a later time, respectively. If "restart later" is selected, the configuration must be saved (either manually or using the save on exit functionality).

(put other AT research here)

## Other

I would like to convince Ember to do the correct thing without discussing the non-technical parts of this issue, namely:

- socio-economic status of people with disabilities (in the world at large, in first-world countries vs others), and how that determines who "gets to" use the web and who doesn't
- accessibility testing and lawsuits in countries that provide legal protection for people with disabilities
