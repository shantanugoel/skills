# Design language

<One paragraph: visual aesthetic, core UX principles (3–5), and explicit anti-patterns to avoid.>

## Users, devices and accessibility

- **Users:** <primary user roles and context>
- **Devices and viewports:** <primary screen sizes and input modes: touch, keyboard, pointer>
- **Accessibility:** <contrast target, keyboard navigation, focus visibility, screen-reader norms>

## Tokens

Once code exists, link the real theme/CSS token file here instead of duplicating raw values.

- **Color roles:** surface, elevated surface, primary/muted ink, border, accent, semantic (`success`, `warning`, `error`), light/dark mode policy.
- **Typography:** font families, size/weight hierarchy, monospace usage.
- **Spacing, radius and elevation:** base grid unit, density, corner radii, shadow/border treatment.
- **Motion:** duration/easing norms and reduced-motion behavior.

## Layout and navigation

- **Shell:** <top-level frame, sidebar/header/tabs, max content width>
- **Hierarchy:** <one primary action per view, grouping, responsive collapse rules>

## Component patterns and states

- **Primitives:** <standard buttons, inputs, tables, dialogs, toasts — link code once built>
- **Empty state:** <how missing data is shown and what action it offers>
- **Loading / busy state:** <skeleton, spinner, or optimistic pattern>
- **Error state:** <inline vs banner, recovery action, plain-language rule>
- **Destructive / confirm:** <when confirmation is required and how it is styled>
- **Done / success:** <feedback pattern>

## Voice and copy

- **Tone and casing:** <sentence case vs title case, direct verbs, button label style>
- **Messages:** <how errors, hints, and confirmations are phrased>

## Choices

Key visual or UX decisions that are expensive to reverse, with rejected alternatives.

- **<Choice>.** <Reason.> We did not use <option>, because <reason>.
