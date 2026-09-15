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

## Frame mapping formula

Scroll progress selects the frame directly. There is no playback, no autoplay, no interpolation between frames — the frame is a pure function of scroll position.

```text
frameIndex = round(progress * (totalFrames - 1))
```

Example with 300 frames (frame 000 to frame 299):

```text
progress 0.00 → frame 000
progress 0.25 → frame 075
progress 0.50 → frame 150
progress 0.75 → frame 225
progress 1.00 → frame 299
```

Clamp `frameIndex` to `[0, totalFrames - 1]` and skip the draw call if the computed index has not changed since the last scroll tick — this alone removes most redundant canvas repaints.

## Deciding the frame count

Do not pick a frame count arbitrarily (e.g. "300 frames because that's a common example") and then force the animation to fit it. Plan frame count and scroll distance together, before any video is produced:

1. How long is the scroll distance for this section, in viewport heights or pixels?
2. How fast should the motion read — a quick beat or a slow reveal?
3. How smooth must it feel? Fast subject motion needs more frames per second of perceived motion than a slow drift.
4. How much asset weight is acceptable for the target devices and network?
5. What is the weakest device/network this experience must still work well on?

A useful starting heuristic: 20–40 effective frames per second of *perceived* motion time is smooth for most subject motion; slower, more graphic sequences can look intentional at 10–15. A 4-second perceived sequence rarely needs more than 80–120 frames even if the source video runs at 30 or 60 fps — extract only the frames the scroll distance can actually resolve, not every source frame.

If the resulting asset budget is still too large, reduce frame count or resolution before shipping — never fix it by silently dropping frames at runtime in a way the design wasn't planned around.

## Loading strategy for large sequences

Choose the delivery strategy based on sequence size and hardware target, not by default:

- **`<img>` swapping** — simplest, fine for smaller sequences (roughly under 60–100 frames) or when frames are small.
- **Sprite sheets** — pack frames into a grid of a few large images instead of many small requests; good when frame count is moderate and dimensions are fixed.
- **Canvas + `ImageBitmap`** — required for large sequences where drawing has to be fast and memory-controlled; decode off the main thread with `createImageBitmap` and draw the current bitmap each `requestAnimationFrame`.
- **Chunked/progressive loading** — load a first usable window of frames (e.g. the first 10–20%) before enabling scroll-driven playback, then continue loading the rest in the background, prioritizing frames near the current scroll position.

Never fetch the entire sequence up front when it is large. Preload a window around the current frame, evict frames that are far from the current position on memory-constrained devices, and always keep a static fallback frame visible while loading.

See `references/ai-video-pipeline.md` for how a frame sequence like this is produced from an AI-generated video.
