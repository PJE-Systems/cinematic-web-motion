# Canvas Frame Sequences

## When to use

Use a frame sequence when exact visual control is more important than video playback.

This works especially well for:

- product renders
- automotive sequences
- camera pullbacks
- controlled 3D renders
- image-based cinematic transitions

## Architecture

Conceptually:

```text
Scroll Progress
      ↓
Frame Index
      ↓
Image Cache
      ↓
Canvas Renderer
```

## Loading strategy

Do not eagerly download hundreds of large frames.

Use:

1. poster
2. first critical frames
3. nearby-frame preload
4. progressive loading
5. fallback if loading fails

## Rendering

Use a single canvas where possible.

Draw only the required frame.

Use requestAnimationFrame to avoid excessive rendering.

## Image format

Prefer modern formats such as:

- AVIF
- WebP

Choose based on browser support and actual file size.

## Memory

Large sequences can consume significant memory.

Consider:

- lower resolution
- fewer frames
- selective preloading
- releasing distant images
- alternative video delivery

## Responsive

A separate lower-resolution sequence can be appropriate for mobile.

Do not automatically send desktop-sized frames to a phone.
