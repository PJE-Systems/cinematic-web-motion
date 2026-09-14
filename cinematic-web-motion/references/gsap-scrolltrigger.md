# GSAP + ScrollTrigger

## When to use

Use GSAP + ScrollTrigger for complex scroll timelines, pinning, sequencing and synchronized transforms.

## Principles

Keep timelines readable.

Prefer one main timeline for a cinematic scene over dozens of unrelated ScrollTriggers.

Group related animation:

- camera
- subject
- environment
- overlay
- UI transition

## Typical structure

Conceptually:

```ts
const timeline = gsap.timeline({
  scrollTrigger: {
    trigger: section,
    start: "top top",
    end: "+=3000",
    scrub: true,
    pin: true,
  },
});
```

Use actual project conventions and installed versions.

## React/Next.js

When using React:

- create timelines after DOM refs exist
- scope selectors to the component
- clean up on unmount
- avoid manipulating React state every animation frame

Use refs for high-frequency animation.

Do not trigger React re-renders for every scroll tick.

## Performance

Prefer:

- transform
- opacity
- scale
- rotation

Be careful with:

- filters
- large blur radii
- layout properties
- expensive SVG operations
- excessive simultaneous animations

## Reduced motion

Respect `prefers-reduced-motion`.

A reduced-motion path should skip or simplify the timeline while leaving content visible.

## Important

Do not add GSAP simply because it is installed. Use it when timeline control provides real value.
