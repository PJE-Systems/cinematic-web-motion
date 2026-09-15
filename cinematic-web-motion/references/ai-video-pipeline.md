# AI Video → Scroll Animation Pipeline

## Principle

An AI-generated video is rarely the final deliverable. It is usually raw material for a frame sequence that scroll will control. Think in this pipeline, not in "generate a video and drop it in a `<video>` tag":

```text
Reference
  → Creative direction
  → UI layout / text position
  → Key visual
  → Subject isolation
  → Video prompt (see references/video-prompt-engineering.md)
  → AI video (KIE Creative MCP)
  → Best variant selected
  → Frame rate conformed
  → Exact frame count extracted
  → Frames optimized for web
  → Scroll-scrubbing implemented
  → Pinning implemented
  → Section handoff implemented
  → Web/UI overlay implemented
  → Mobile fallback implemented
  → Performance verified
```

Critically, UI layout and text position are decided **before** the video prompt is written, not after the video exists. See "Design-first ordering" in `references/video-prompt-engineering.md`. A video generated without knowing where the headline, subtext and CTA will sit almost never composes cleanly with them afterward.

Only use a plain `<video>` element with normal autoplay/controls when the sequence genuinely should just play back (e.g. an ambient loop, a testimonial). If the sequence needs to feel directed by the visitor's scroll, it needs to become a frame sequence, not a playing video.

## When to reach for the KIE Creative MCP

Use the project's KIE Creative MCP (image/video generation) when a cinematic section needs a visual asset that does not exist yet:

- a hero subject (product, character, vehicle, environment) with no usable photography/footage
- a specific camera move or transformation that would be expensive to film or model in 3D
- a stylized key visual to establish art direction before committing to a full build
- multiple exploratory variants of a shot to compare before picking a direction

Do not reach for it to generate filler decoration, generic backgrounds, or stock-photo replacements that add no story value — that produces the exact generic-AI-slop aesthetic this skill exists to avoid.

## Step-by-step workflow

1. **Define the visual concept.** What does this scene need to communicate? Revisit the story design (`references/story-design.md`) before generating anything.
2. **Analyze any reference.** If the user supplied a design or brand reference, study its layout, subject framing, color, lighting and camera language before generating — see "References" in the main SKILL.md.
3. **Determine the UI layout and text position first.** Before writing any prompt, know where the headline, subtext, CTA and animated subject will sit, which regions must stay visually quiet, and whether that reserved area moves during the sequence. See "Design-first ordering" in `references/video-prompt-engineering.md`. Do not generate the video and try to find room for text afterward.
4. **Generate a key visual (still image).** Establish look, subject, lighting and composition — including the reserved UI-safe area — as a still before spending video generations on it. Iterate here — it's cheaper than iterating on video.
5. **Isolate the subject** from the key visual if the subject needs to move, scale or hand off independently of its background (see below). Prefer producing an isolated/transparent subject before animating it.
6. **Write the video prompt.** Build a full, production-grade prompt covering subject, starting position, action, body mechanics, camera, composition, UI-safe areas, lighting, environment, temporal progression and ending state — never a one-line description. Follow the structure and camera vocabulary in `references/video-prompt-engineering.md`. Never ask the model to render headline/CTA/UI text into the footage.
7. **Generate the video via the KIE Creative MCP.** For hero or scroll-critical sequences, produce a deliberately varied small set of variants (e.g. calmer / more dynamic / different camera) rather than accepting the first result or retrying the same prompt near-identically.
8. **Select the best variant** against the actual website composition, not in isolation: does it work with the planned overlay, is the motion clean and continuous, are the start/end states strong, does it still read well scrolled slowly or in reverse? See "Generating and selecting variants" in `references/video-prompt-engineering.md`.
9. **Conform the frame rate** to what the sequence actually needs — resample the source video to the target fps rather than assuming its native fps is correct for this use.
10. **Extract exactly the planned number of frames** (see the frame-count planning method in `references/image-sequences.md`) — decide the count from the scroll distance and motion pacing first, then extract, not the other way around.
11. **Optimize frames for the web** — WebP or AVIF, resolution matched to actual rendered size (including a lower-resolution mobile set), stripped metadata.
12. **Implement scroll-scrubbing** against the frame sequence (`references/image-sequences.md`, `references/scroll-animation.md`).
13. **Implement pinning** for the section if the narrative calls for the scene to hold in place while the timeline advances (`references/scroll-animation.md`).
14. **Implement the web/UI overlay** — real HTML/CSS headline, subtext and CTA placed into the UI-safe area the video was prompted to reserve, timed against the same scroll progress as the frame sequence if the text itself animates (`references/typography-motion.md`).
15. **Implement the section handoff** into whatever comes next (`references/transitions.md`).
16. **Implement a mobile fallback** — do not ship the desktop frame count/resolution unchanged (`references/mobile.md`).
17. **Test performance** — load time, memory, frame-rate smoothness, on a representative mid-tier device, not only on the development machine.

Do not skip from step 7 straight to implementation. A video that "looks fine" on its own can still be unusable for scrubbing or unusable with the planned overlay if its motion or composition doesn't match the mapped scroll timeline and UI-safe area — verify against the plan before extracting frames.

## Subject isolation

Before animating a character, product, vehicle or other focal subject, consider whether it should be separated from its background rather than animated as part of one flat scene.

Flat (harder to work with):

```text
Layer: person + background + text + UI, all baked into one image/video
```

Layered (preferred when the subject needs independent motion):

```text
Layer 1 — Background (environment, gradient, generated scene)
Layer 2 — Typography (headline, kinetic text)
Layer 3 — Subject (character / product / vehicle, isolated with alpha)
Layer 4 — Decorative/foreground elements
```

Benefits of isolating the subject:

- it can scale, translate and rotate independently of the background timeline
- it can be pinned while the background continues to change behind it
- it can hand off between sections (see `references/transitions.md`) without dragging its original background along
- text can be placed behind or in front of it correctly, at any scroll position, without re-compositing

When the subject comes from an AI-generated video, isolate it as early as possible in the pipeline — ideally by generating or extracting it against a clean/removable background before the frame sequence is produced, rather than trying to key it out of a busy generated background after the fact. If clean isolation isn't achievable from the model output, treat the whole shot as one flat layer rather than faking isolation with a rough cutout — a bad cutout looks worse than no isolation.

## Asset quality discipline

Generated media should serve the design, not visibly announce itself as generated:

- never let the video model render UI text, headlines, subtext, buttons or logos inside the footage — this is a hard rule, not a preference; render all real brand/UI text as HTML/SVG on top, and write the prompt so the model never needs to be told to draw it (see `references/video-prompt-engineering.md`)
- check frame-to-frame continuity — a subject that subtly morphs or changes proportions across the sequence will read as broken once frame-stepped by scroll (scroll-scrubbing exposes inconsistencies that normal playback speed hides)
- keep camera direction and lighting consistent across variants that will be used together in the same sequence
- favor continuous, single-shot motion over multi-cut footage — a scroll-scrubbed sequence lets the visitor move forward and backward through time, and cuts make that disorienting
