layout: post
title: 'Improving accessibility with accessibility acceptance criteria'
tags:
  - gds
  - accessibility
categories:
  - projects
date: 2017-07-29
---

Accessibility acceptance criteria are a list of criteria that a user interface must meet to be considered accessible. They define what makes the building blocks of a user interface accessible and give teams criteria to test against. They a place to record accessibility decisions.

[As Alistair Duggan said](https://accessibility.blog.gov.uk/2016/05/16/what-we-mean-when-we-talk-about-accessibility-2/):

> it is lack of awareness that most commonly results in things being inaccessible

Accessibility acceptance criteria raise awareness about what accessible means in a specific context. They’re more specific than general accessibility guidance, such as the Web Content Accessibility Guidelines (WCAG).

At Government Digital Service what we build must be accessible. It’s one of our design principles, “[This is for everyone](https://www.gov.uk/design-principles#sixth)”:

> Accessible design is good design. Everything we build should be as inclusive, legible and readable as possible. [...] The people who most need our services are often the people who find them hardest to use. Let’s think about those people from the start.

By defining accessibility acceptance criteria upfront we are forced to think about accessibility from the start. It helps us to [consider the range of users](https://accessibility.blog.gov.uk/2016/05/16/consider-the-range-of-people-that-will-use-your-product-or-service/). The criteria become a starting point for building accessible things.

## Example criteria

### Accessible autocomplete

At GDS we first used accessibility acceptance criteria when building the [accessible autocomplete](https://github.com/alphagov/accessible-autocomplete). Theodor Vararu, Léonie Watson and Ed Horsford defined the following [autocomplete accessibility criteria](https://github.com/alphagov/accessible-autocomplete/blob/master/accessibility-criteria.md) — the necessary behaviours that an autocomplete needs to meet to be usable by assistive technologies:

> The field with autocomplete must:
> 1. Be focusable with a keyboard
> 2. Indicate when it has keyboard focus
> 3. Inform the user that it is an editable field
> 4. Inform the user if there is a pre-filled value
> 5. Inform the user that autocomplete is available
> 6. Explain how to use autocomplete
> 7. Inform the user that content has been expanded
> 8. Inform the user when there are matches, or if there are no matches
> 9. (Optional) Inform the user how many matches are currently available
> 10. Inform the user as the number of matches changes
> 11. Enable the user to navigate the available matches using touch or keyboard
> 12. Inform the user when a match is selected
> 13. (Optional) Inform the user which number the currently selected match is (1 of 3 for example)
> 14. Inform the user if a match is pre-selected
> 15. Enable the user to confirm the selected match
> 16. Inform the user when a match is confirmed
> 17. Return focus to the editable field when a selected match is confirmed

### GOV.UK publishing components

On the GOV.UK Publishing Frontend team we are breaking down our pages into reusable component blocks which are documented in a component guide. A component is a package comprised of template, style, behaviour and documentation that follows our [component principles](https://github.com/alphagov/govuk_publishing_components/blob/master/docs/component_principles.md).

We are defining accessibility acceptance criteria for each component to help us assess the accessibility of the existing code and to ensure we can iterate on these component designs without breaking accessibility.

Our components are less complex than an autocomplete, but our criteria still highlight important accessibility needs.

#### Navigating translations

For a component that lists links to translations of the current page we identify the following criteria:

> The translation navigation links must identify the language of the link for correct screen reader pronunciation

While this is true for all words that are in a language different to the main content’s language, it is especially important to consider in the context of this component. Here there is a high risk of introducing an accessibility barrier.

#### Banners

On a banner component that places white text on a blue background we use the criteria to highlight the importance of contrast ratios:

> The banner must have a text contrast ratio of at least 4.5:1 against the background colour to meet [WCAG AA](https://www.w3.org/TR/WCAG20/#visual-audio-contrast-contrast)

While all text must have a sufficient contrast ratio, given this component’s use of colour it has an increased risk of introducing a barrier.

Note also that WCAG AA defines different ratios for large and small text, we’ve found that the definition of large and small can be misinterpreted. Using one contrast ratio for all text eliminates any chance of mistake.

## Criteria maintain accessibility

When building user interfaces we do our best to ensure they are accessible. But without a definition of what made it accessible it’s hard to iterate on and too easy to introduce accessibility regressions. Even when we know it’s been built well, and that effort went into making it accessible – how do we make changes without breaking accessibility? What stops our new definition of accessibility from being incomplete or different to the original definition?

Making something accessible can be nuanced and complex and [not all accessibility testing can be automated](https://blog.vararu.org/accessibility-testing-tools-are-lying-to-you/). There are always manual steps needed to test features in the way they impact users.

Outlining accessibility issues in criteria records the decisions that were made and define the rules that keep something accessible.

In code we can use these criteria to write unit tests that prevent regressions. In our translation component we can test that links have a `lang` attribute, and in our banner component we can [test the contrast ratio](https://github.com/alphagov/govuk_frontend_toolkit/pull/374).

## Writing accessibility acceptance criteria

### Start with accessibility needs

Identify where there is a high risk of introducing an accessibility barrier and include criteria that prevent them.

If similar things already exist, review them to find barriers. Test them with users who have access needs. The original criteria for the accessible autocomplete were derived from tests made by Theodor Vararu on existing autocomplete libraries.

For many patterns the hard work of defining what accessible means has been documented in guidelines like WCAG. Do the hard work to extract rules specific to what you’re building and link back to the guidelines to give context. Consider which rules are most easily broken and give them prominence.

### Don't be too generic

Criteria are useful if they are specific and testable.

When we began writing accessibility acceptance criteria for components we had difficulty knowing what to include. Consider a component that contains links – do the criteria need to list everything that make a link accessible? How much of this becomes a reproduction of existing guidelines?

In this case it was helpful to create a shared definition of an accessible link that could be linked to. This avoided diluting the criteria while giving us a place to record more generic decisions.

### Iterate criteria

As something is built and tested, continue to refine your criteria as you find missing needs. When accessibility bugs are found – a browser bug, a screen reader quirk, new technology misbehaving, add further criteria and treat them like a failing unit test.

### Separate guidance and accessibility acceptance criteria

Guidance is for users, accessibility acceptance criteria are for maintainers.

Not everything is under your control. For instance, some of our components may become inaccessible if they’re passed certain parameters. Consider a contrived example of the translation component being passed data that says a link is in English but on inspection actually reads in Arabic.
