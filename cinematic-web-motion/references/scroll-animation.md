# Scroll Animation Architecture

## Principle

Treat scroll as a timeline.

Normalize scroll progress:

`0 = start`
`1 = end`

Map progress into scene ranges.

Example:

- 0.00-0.15 establish
- 0.15-0.30 movement
- 0.30-0.45 disruption
- 0.45-0.60 freeze/reveal
- 0.60-0.80 scale
- 0.80-0.95 resolution
- 0.95-1.00 CTA transition

## Prefer deterministic animation

Animation should be derived from scroll progress rather than accumulated state.

Good:

`state = interpolate(progress)`

Avoid:

`state += delta` on every scroll event.

Deterministic mapping prevents jitter and makes seeking predictable.

## Pinning

Pin a cinematic scene when the visual narrative needs to remain in place while the timeline advances.

The surrounding page should still have a normal document flow.

Do not pin huge portions of the website without a clear reason.

## Scrubbing

When using a scrubbed animation:

- map progress to a known timeline
- keep interpolation smooth
- avoid excessive easing that makes scroll feel disconnected
- ensure the final state is reached exactly

## Cleanup

When a component unmounts:

- remove listeners
- kill animation timelines
- cancel animation loops
- dispose renderer resources
- release references to large media buffers when possible

## Responsive ranges

Do not assume desktop scroll distances work on mobile.

Use responsive configuration where necessary.
