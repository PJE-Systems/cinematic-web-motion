# Typography Motion / Kinetic Typography

## Principle

Treat typography as a designed, animatable element of the story, not just text that happens to fade in. But motion on text must still serve reading — it can never make the content harder to parse or slower to consume than static text would be.

## Techniques

- **Character-by-character reveal** — each glyph animates in with a small stagger. Use for short, high-impact headlines; avoid on paragraph-length text, where it becomes slow and annoying to wait through.
- **Word-by-word reveal** — coarser than character reveal, reads faster, works for longer headlines and subheadings.
- **Line reveal** — each line masks/clips in as a unit; good for multi-line headlines where the whole line should feel like one beat.
- **Masked/clip-path reveal** — the text is revealed through an animated clip-path or mask edge, giving a "wipe" feel rather than a fade.
- **Split-text scroll binding** — split into characters/words/lines and bind each unit's progress to scroll position instead of time, so revealing is scroll-driven rather than autoplaying once in view.
- **Blur-to-sharp** — text enters blurred and resolves to sharp focus; reads as a "coming into focus" beat, pairs well with camera-focus metaphors elsewhere in the scene.
- **Scroll-based scale/opacity** — heading scales or fades as a function of scroll progress, often used for a hero headline that recedes as the visitor continues past it.
- **Variable font animation** — animate weight/width/optical-size axes of a variable font for a subtler, more typographic motion than transform-based effects; good for premium, editorial-feeling brands.

## When to use which

Match the technique to the beat it serves in the story mapping (see "Animation mapping" in the main SKILL.md):

- A hero's opening statement: word or line reveal, once, on entry — not on every scroll tick.
- A scroll-scrubbed section transition: bind opacity/position/clip directly to scroll progress so the text's state is always a deterministic function of scroll, matching the rest of the scene.
- Supporting body copy: usually no motion beyond a simple fade/translate on first appearance. Never character-stagger long-form copy — it punishes the reader.

## Restraint

Kinetic typography is one of the easiest cinematic techniques to overuse. Guardrails:

- Animate a heading or key statement, not every paragraph and every list item.
- One reveal style per section is usually enough; mixing several kinetic techniques in the same viewport reads as noisy rather than sophisticated.
- Once text has finished revealing, it should be genuinely stable — no residual jitter, no re-triggering the reveal if the user scrolls slightly up and back down, unless that reversal is an intentional part of a scrubbed timeline.
- If `prefers-reduced-motion` is set, replace reveals with the final, fully visible state immediately — see `references/accessibility.md`.

## Implementation notes

- Split text into spans for character/word effects at build time or on mount, not by re-parsing on every render.
- Prefer `transform` and `opacity` for the animated properties (GPU-friendly) over animating `width`, `letter-spacing`, or other layout-triggering properties per frame.
- For scroll-bound text, drive it from the same progress value the rest of the section uses — do not give text its own independent scroll listener with different easing than the visuals it's paired with.
- Keep the underlying text as real, selectable, crawlable HTML at all times — splitting into spans for animation must not remove it from the accessibility tree or break screen readers (use `aria-label` on the container with the full string when splitting into individual character spans).
