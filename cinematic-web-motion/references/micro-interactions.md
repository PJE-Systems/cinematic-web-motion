# Micro-Interactions & Cursor

## Principle

Micro-interactions are the small-scale counterpart to the cinematic macro story: they should feel intentional, subtle and premium, not flashy. They confirm that the interface is alive and responsive — they are not the main event.

## Where to use them

- buttons and primary CTAs
- links (especially inline text links and nav items)
- cards (product, service, portfolio items)
- navigation and menus
- form inputs and focus states
- cursor-following or cursor-reactive elements

## Common patterns

- **Magnetic button/link** — the element subtly translates toward the cursor within a small radius as the cursor approaches, and springs back on leave. Keep the pull distance small (a few pixels to ~15% of the element's size) — an exaggerated pull feels gimmicky rather than premium.
- **Subtle scale** — a card or button scales by a small amount (roughly 1.02–1.05×) on hover, with a quick, slightly eased transition. Avoid large scale jumps.
- **Underline reveal** — an underline or accent line grows in from one side on hover instead of simply appearing, for text links.
- **Icon movement** — an arrow or icon inside a button/link nudges in the direction of travel (e.g. right on hover for "next" actions).
- **Hover image reveal** — a thumbnail or preview image reveals/crossfades in near the cursor when hovering a related text item (common in editorial/portfolio listings).
- **Cursor-following elements** — a custom cursor or cursor-adjacent element (a label, a play icon) that follows pointer position with slight lag/easing rather than 1:1 tracking, which reads as more natural.
- **Input focus states** — label or border animates on focus with a quick, clear transition; never rely on color change alone for the state.

## Motion quality bar

- Use short durations (roughly 150–350ms) and an easing curve with a slight deceleration (`ease-out`-style) for most micro-interactions — linear motion on small UI elements reads as robotic.
- Debounce/throttle cursor-following effects to animation frames, not raw `mousemove` events, to avoid jank.
- Every hover effect needs a matching, equally smooth reverse/leave transition — a hover state that snaps back abruptly undoes the quality of the entrance.
- Micro-interactions must not block or delay the actual interaction (a click should register immediately even mid-animation).

## Accessibility and input method

- Cursor-following and magnetic effects only apply to devices with real pointer input (`@media (hover: hover) and (pointer: fine)`) — they should not attempt to run on touch devices where there is no persistent cursor.
- Keyboard focus must trigger an equivalent, clearly visible state to hover — do not build an interaction that only fires on `:hover` and provide no `:focus-visible` equivalent.
- Respect `prefers-reduced-motion`: keep the functional state (hover/focus/active) but drop translation-heavy effects like magnetic pull; simple opacity/color changes are generally fine to keep.

## Restraint

Not every element needs a custom interaction. Reserve magnetic and cursor-following effects for a small number of high-visibility elements (primary CTA, hero navigation) — applying them everywhere dilutes the effect and adds unnecessary event listeners across the page.
