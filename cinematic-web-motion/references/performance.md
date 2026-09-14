# Cinematic Performance

## Principle

A cinematic website that stutters is not premium.

Measure and optimize actual bottlenecks.

## Media

Optimize:

- video bitrate
- image dimensions
- frame count
- texture resolution
- compression
- loading priority

Do not ship production-sized source assets when a smaller asset looks identical on the target screen.

## Animation

Prefer compositor-friendly properties:

- transform
- opacity

Avoid unnecessary layout recalculation.

## Canvas

- render only when necessary
- use requestAnimationFrame
- avoid expensive per-frame allocations
- keep canvas resolution reasonable
- consider device pixel ratio limits

## Three.js

- keep scene complexity low
- reuse materials
- avoid unnecessary lights
- compress textures
- use instancing when useful
- dispose geometries/materials/textures
- reduce pixel ratio on weaker devices

## Loading

Use progressive loading.

The first meaningful page content should not depend on a large cinematic asset.

## Mobile

Assume mobile has less GPU and memory headroom.

A simplified cinematic experience is better than a technically identical but unusable one.

## Monitoring

When possible check:

- frame rate
- long tasks
- memory pressure
- network transfer
- largest contentful paint
- interaction responsiveness

Do not optimize based only on assumptions.
