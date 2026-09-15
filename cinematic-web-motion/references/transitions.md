# Cinematic Transitions

## Principle

Transitions should explain relationships.

The strongest transitions transform one concept into another.

## Good transitions

### Scale

Close-up object → entire environment.

### Morphological relationship

Wheel → circular network node.

### Spatial continuity

Camera leaves one scene and enters another.

### Freeze

Real-world movement stops, allowing the brand/solution to enter.

### Pullback

A local problem becomes a system-level view.

### Re-entry

After showing the system, the camera returns to the original subject.

## Weak transitions

Avoid:

- random glitch
- random particles
- generic zoom
- excessive blur
- unnecessary lens effects
- arbitrary color explosions
- unrelated 3D shapes

## Section handoffs

A handoff is a transition where an element visually survives the boundary between two sections instead of the page cutting from one static section to the next.

Common handoff patterns:

- **Subject handoff** — the pinned hero's subject (character, product, vehicle) moves toward the edge of its scene as scroll progress approaches 1.0, and the next section picks it up already in motion (same element via shared layout/FLIP, or a matched re-entry animation using the same scale/position).
- **Typography handoff** — the outgoing section's heading shrinks, fades or slides to a position the incoming section's heading continues from, so the reader's eye is never asked to jump.
- **Background handoff** — the background color/gradient/image of the outgoing section bleeds into or morphs toward the incoming section's background instead of hard-cutting.
- **Progress handoff** — the pinned section unpins only once its internal timeline reaches 1.0, and the next section's entrance animation begins from that exact point rather than from an arbitrary independent scroll trigger.

Plan the handoff as part of the animation mapping (see the main SKILL.md "Animation mapping" section), not as an afterthought once both sections already exist. Decide, before implementing either section: what crosses the boundary, in what state does it arrive, and where does it come to rest.

A hard, unrelated cut between sections is acceptable when there is no meaningful visual or narrative relationship to carry across — do not force a handoff where none is justified.

## Text transitions

Text should appear because the narrative reached a point where the information is useful.

Do not animate every word independently.

Use:

- controlled reveal
- opacity
- small translation
- scale
- clipping/masking

Keep text readable and stable.
