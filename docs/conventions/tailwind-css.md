# Tailwind CSS Conventions

Use Tailwind as the default styling mechanism when the project uses Tailwind.
Avoid custom CSS when Tailwind expresses the requirement clearly and maintainably.

## Tokens first

Prefer established theme/design tokens over arbitrary values.

Prefer:

```text
p-4
gap-6
text-base
rounded-lg
```

instead of unnecessary one-off values such as:

```text
p-[17px]
gap-[23px]
text-[15px]
```

When a project needs a repeated value that Tailwind does not provide, define a project token rather than repeating arbitrary values.

## Design token template

Each project should define its own design language for at least:

```text
Colors
- background
- foreground
- primary
- secondary
- muted
- destructive
- border
- accent

Typography
- font families
- heading scale
- body scale
- label/caption scale

Spacing
- standard content spacing
- section spacing
- container widths

Shape
- radius scale
- border rules

Elevation
- shadow scale

Motion
- duration
- easing
```

Do not invent random tokens inside components when an equivalent project token already exists.

## Responsive design

Use mobile-first styling.

```text
grid-cols-1 md:grid-cols-2 lg:grid-cols-3
```

Start with the base/mobile experience and add larger breakpoint enhancements.

## Class organization

Keep classes logically ordered when automatic sorting is unavailable:

1. layout / display
2. position
3. sizing
4. spacing
5. typography
6. background
7. border
8. effects
9. interaction/state
10. responsive modifiers

Prefer automatic Tailwind/Prettier sorting when the project already uses it.

## Components and variants

When visual patterns repeat, prefer reusable components and variants:

```tsx
<Button variant="primary" />
```

instead of duplicating large class lists or relying heavily on `@apply`.

Use `cn()` for conditional class composition.
Use `cva()` or an established equivalent when components have multiple structured variants.
Do not introduce variant abstractions for trivial one-off components.

## Accessibility

Mandatory UI requirements:

- visible focus states
- sufficient contrast
- semantic HTML
- keyboard navigation
- reduced-motion awareness
- proper labels for controls

Styling must not remove accessible browser behavior without an equivalent replacement.
