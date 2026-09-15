# Video Prompt Engineering for Web-Bound AI Assets

## Principle

An AI-generated video that will live inside a website is not a standalone clip — it is an **interactive web design asset**. It must be prompted with the website's layout, UI overlay and scroll behavior already in mind, not generated first and fitted to the design afterward.

Never write a short, generic prompt like `"Person walks through a modern office"` for a web-bound video. Write a structured, production-grade prompt that specifies exactly what moves, what stays still, what the camera does, and which areas of the frame must stay visually quiet for the UI that will sit on top of it.

This file governs how to *write the prompt* handed to the video model via the project's KIE Creative MCP (`pje-creative`). For the surrounding production pipeline (frame extraction, scrubbing, pinning, handoff), see `references/ai-video-pipeline.md`.

## Hard rule: never let the video model render UI text

Headlines, subheadlines, buttons, labels and any other UI copy must never be generated inside the video. The video model produces the visual scene only; real text is layered on top afterward as HTML/CSS.

This is not optional and is not a style preference — a video with baked-in text cannot be localized, cannot be made accessible, cannot be updated, and will almost always render text with visible AI artifacts. Every prompt must be written so composition and motion leave the planned text area clean, without ever asking the model to draw the text itself.

## Design-first ordering

Determine the UI layout before writing the video prompt — never the reverse.

```text
Design
  → UI layout
  → Text position (headline / subtext / CTA)
  → Visual composition
  → Video prompt
  → AI video (KIE Creative MCP)
  → Web overlay
```

Not:

```text
AI video
  → try to fit text on top afterward
```

Before writing any prompt, answer:

1. Where does the headline sit?
2. Where does the subtext sit?
3. Where does the CTA sit?
4. Where does the animated subject sit, and how does that change over the sequence?
5. Which side/region of the composition needs to stay visually quiet?
6. Does that reserved region move over time, or stay fixed?
7. Will the UI itself be static, or animated on its own scroll/timeline (see `references/typography-motion.md`)?
8. Does the subject need to avoid a specific region throughout its motion, not just at rest?

The answers become explicit constraints in the prompt — not an afterthought "leave space for text" tacked onto the end.

## Prompt structure

Compose the prompt internally around this schema before writing the final natural-language version:

1. **Scene** — what is this shot, in one sentence
2. **Subject** — who/what, appearance, wardrobe/material, proportions
3. **Starting position** — exact position and pose in frame at time 0
4. **Action** — what the subject does over the sequence
5. **Body mechanics** — natural weight shift, gait, deceleration, realism cues (for characters); mechanical/material behavior (for products)
6. **Camera** — camera type and behavior (see camera vocabulary below)
7. **Composition** — framing, rule-of-thirds placement, where the subject sits in the frame and how that changes
8. **Spatial layout / UI-safe areas** — which regions must stay clean, low-detail, and low-contrast for a text or CTA overlay, and for how long during the sequence
9. **Lighting** — direction, quality (soft/hard), color temperature, how it interacts with the UI-safe area's contrast
10. **Environment** — setting, depth, background elements, what must remain static in the background
11. **Visual style** — cinematic look, color grade, lens character, material rendering
12. **Temporal progression** — the sequence described as a timeline: start → motion → deceleration/settle → end
13. **Ending state** — precise description of the final frame's composition and pose
14. **Continuity requirements** — screen direction, subject scale, horizon line, lighting direction, anything that must match an adjacent section's video (see "Spatial continuity across sections" below)
15. **Relevant negative constraints** — only the ones that actually matter for this shot (see below)

Despite this internal structure, the prompt handed to the model must read as one coherent, natural creative brief — not a labeled JSON-like list. Fold the 15 points into flowing prose the way a director would brief a cinematographer.

### Example: bad vs. good

Bad:

```text
Create a cinematic shot of a businessman walking through a modern office.
```

Good:

```text
Create a cinematic wide composition of a businessman walking slowly from left to
right through a modern architectural office with soft daylight from large windows.
At the beginning, he is positioned near the lower-right area of the frame and
remains almost still for a brief moment. He then begins walking naturally toward
the center-right with subtle weight shifts and realistic body mechanics, never
crossing into the left third of the frame. The camera performs a slow, locked
lateral tracking move that keeps his relative framing consistent — no handheld
shake, no sudden reframing. Keep the upper-left third of the composition visually
clean and relatively low-detail and low-contrast throughout the entire sequence,
reserved for a website headline overlay. Maintain clear tonal separation between
the subject and the background so a future overlay stays readable. Do not place
important objects, faces, hands, or high-contrast details inside the reserved
area at any point in the sequence. In the final moments, his movement decelerates
and settles into a stable, readable standing pose on the right side of the frame,
leaving the left side clean and quiet for the next section's headline. No text,
no logos, no UI elements, no additional people.
```

The difference is not length for its own sake — every added sentence encodes a real constraint the web layout needs.

## Temporal description

Describe motion as a timeline, not just a static subject description. This directly determines how well the footage scrubs frame-by-frame later.

Structure:

- **Start state** — exact position, pose and framing at the first frame
- **Motion** — what happens through the sequence, described with pacing (e.g. "remains still briefly, then begins moving with a gradual acceleration")
- **End state** — exact position, pose and framing at the last frame, composed deliberately for whatever comes next (a pinned section's unpin, a handoff, a next section's starting pose)

For scroll-scrubbed sequences specifically, the prompt should push the model toward:

- a clear, readable start state (frame 0 must work as a standalone still, since a visitor can land there via a hard scroll position)
- continuous, uninterrupted motion with no cuts
- no abrupt jumps in position, scale or lighting
- a camera that does not reverse direction or change type mid-shot
- a clear, readable end state suited to whatever the next section is doing

Scrubbing exposes problems that normal playback speed hides — a visitor can move slowly, stop, or reverse through the timeline, so any jitter, inconsistency or morph becomes far more visible than in autoplay.

## Camera vocabulary

Avoid vague camera language like "cinematic camera movement." Choose and name a specific camera behavior, matched to what the web interaction needs:

- slow dolly forward / dolly back
- subtle lateral tracking
- locked-off (static) camera
- slow orbit
- controlled push-in
- crane movement
- low-angle tracking shot
- overhead transition
- gentle parallax
- static camera with subject movement only
- camera follows subject (subject-locked framing)
- camera maintains fixed subject framing throughout

For scroll-scrubbed sequences, prefer camera behaviors that stay legible when played at arbitrary speed and in reverse: locked-off, slow dolly, subtle tracking, controlled push-in. Avoid whip pans, handheld shake, rapid reframing or direction changes — they read as broken rather than cinematic once the visitor controls playback speed via scroll.

## Spatial continuity across sections

When a website uses more than one AI-generated video across adjacent sections, they should read as one continuous scene, not a series of disconnected clips. Before prompting each subsequent shot, check it against the previous one for:

- screen direction (a subject moving right should continue moving right, not flip)
- subject position and scale relative to frame
- camera direction and type
- horizon line
- perspective/lens character
- lighting direction and color temperature
- environmental continuity (same implied space, time of day, materials)
- the previous shot's final pose vs. this shot's starting pose

State the connection explicitly in the prompt's continuity section, e.g. "continuing directly from a shot where the subject was walking right at eye-level height with soft daylight from the left — maintain the same lighting direction and walking pace at the start of this shot."

## Isolated-character prompting

When the subject needs to become an independent, isolatable layer (see "Subject isolation" in `references/ai-video-pipeline.md`), prompt specifically for clean separation:

- clean, simple or removable background
- clear silhouette against the background at every frame
- full body visible, no limbs cropped by the frame edge
- no important objects overlapping or occluding the subject
- consistent wardrobe and proportions across the whole sequence
- controlled, moderate-speed motion (extreme motion blur defeats clean matting)
- strong tonal/color separation between subject and background

## Negative constraints

Add negative instructions only when they matter for the specific shot — do not append a boilerplate block of every possible constraint to every prompt.

Common, frequently-relevant constraints:

- no text, no subtitles, no captions
- no logos
- no UI elements
- no typography
- no extra people
- no unnecessary camera shake
- no sudden camera movement
- no object deformation
- no limb distortion
- no changing clothing
- no changing environment
- no unnecessary background movement

Choose the subset that's actually at risk for this shot. A locked-off product shot doesn't need "no camera shake" spelled out as urgently as a walking-character shot does; a single-subject shot may not need "no extra people" if the setting makes that implausible.

## Use-case prompt profiles

Recognize which of these the current shot is, and weight the prompt accordingly:

### Cinematic hero
Emphasize: strong, deliberate composition; slow, controlled camera; high-quality light; a clear hero framing; an explicit UI-safe area for the primary headline and CTA.

### Scroll-scrub character
Emphasize: continuous, natural motion; explicit start/end poses; a stable, non-reversing camera; realistic body mechanics; precise spatial positioning that supports frame-accurate scrubbing.

### Product showcase
Emphasize: product form and materiality; a controlled, often locked or slow-orbit camera; a clean, unbroken silhouette; the product fully in frame at all times; a UI-safe area for spec copy or CTA.

### Section transition
Emphasize: a start state that matches the previous section's end state; a clearly defined motion direction; a clearly defined end state suited to the next section; spatial continuity; a clean handoff moment (see `references/transitions.md`).

### Background animation
Emphasize: subtle, low-amplitude motion; minimal visual noise; explicitly no competition with foreground UI; consistently high overlay readability across the entire sequence, not just at one point in time.

## Generating and selecting variants

For a hero or scroll-critical sequence, do not accept the first generated clip. When the KIE Creative MCP allows multiple generations, produce a small set of deliberately different variants — for example a calmer take, a more dynamic take, and one with a different camera choice — rather than several near-identical retries of the same prompt.

Evaluate variants against the actual website composition, not in isolation:

- which version works best with the planned overlay?
- which has the cleanest, most continuous motion?
- which has the strongest start and end state?
- which still reads well if the visitor scrolls slowly or in reverse?
- which produces the clearest visual hierarchy once text and UI are added on top?

Selecting the "best-looking clip on its own" is not the same evaluation as selecting the one that will work once composited with real UI — always judge with the overlay in mind, even if it's only mocked up as a placeholder box during review.

## Model selection

Use whichever video-generation tools and parameters the KIE Creative MCP actually exposes for the task — check available models/parameters via the MCP rather than assuming or inventing endpoints, parameter names, or capabilities that were not confirmed to exist. For premium cinematic web sequences, prefer the highest-quality model the MCP offers that fits the shot's requirements (motion quality, duration, resolution) rather than defaulting to the same model for every use case regardless of fit.

## The core check

Before considering a video prompt finished, ask: **can this footage later be combined with real HTML/UI text and still look like one coherent design?**

If the honest answer is no — the UI-safe area isn't clean enough, the motion crosses into the text zone, the end state doesn't compose well with what comes next — revise the prompt before generating, or regenerate rather than shipping a mismatch and trying to force the UI to work around it.

## Proactive design thinking

Do not wait for an explicit instruction like "leave room for the text." If the website layout implies that text or UI will sit over the video, work through this sequence automatically before writing the prompt:

1. identify the UI position from the layout
2. determine the visual composition that supports it
3. position the subject accordingly
4. plan the negative space needed, including how it must behave over time
5. write the video prompt to encode all of the above
6. define explicit start and end states
7. only then plan the UI's own animation timing (text reveal frames, CTA entrance, etc.)

Treat design and video generation as one combined decision, not two separate tasks handed off between people.
