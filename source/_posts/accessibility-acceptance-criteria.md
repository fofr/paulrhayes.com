layout: post
title: 'Accessibility acceptance criteria'
tags:
  - gds
  - accessibility
categories:
  - projects
date: 2017-07-29
---

Accessibility acceptance criteria are a list of criteria that a user interface must meet to be considered accessible. They define accessible in the context of a design pattern or component and they give developers a set of criteria to test against.

## Define accessible

At Government Digital Service what we build must be accessible. It’s one of our design principles, “[This is for everyone](https://www.gov.uk/design-principles#sixth)”.

> Accessible design is good design. Everything we build should be as inclusive, legible and readable as possible. [...] The people who most need our services are often the people who find them hardest to use. Let’s think about those people from the start.

This thing we’re building, this user interface, this pattern or this component – it must be accessible. What makes it accessible? What does accessible mean in the context of this thing?

Consider something that’s been built already, something we need to change. Even when we know it’s been built well, and that effort went into making it accessible – how do we make changes without breaking accessibility? What stops our new definition of accessibility from being incomplete or different to the original definition?

Accessibility acceptance criteria define what accessible means.

## Example criteria

Accessibility acceptance criteria are a list of things that define what a user interface must do to be accessible. At GDS we first used them when building the [accessible autocomplete](https://github.com/alphagov/accessible-autocomplete).

Theodor Vararu, Léonie Watson and Ed Horsford [defined the following](https://github.com/alphagov/accessible-autocomplete/blob/master/accessibility-criteria.md):

> The field with autocomplete must:
> * Be focusable with a keyboard
> * Indicate when it has keyboard focus
> * Inform the user that it is an editable field
> * Inform the user if there is a pre-filled value
> …
> and [13 more](https://github.com/alphagov/accessible-autocomplete/blob/master/accessibility-criteria.md)

## Changing criteria

* All developers don't know WCAG
* Hard to find everything relating to what you're building in WCAG
* Many things found in research that are nuanced and not in WCAG
* Learnings from research
* Browser bugs and quirks
* When something inaccessible found, new technology or a hidden bug, add criteria and treat like a failing test
* Like a test suite


 [Automated accessibility testing is limited](https://blog.vararu.org/accessibility-testing-tools-are-lying-to-you/).
