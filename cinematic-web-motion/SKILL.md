---
name: cinematic-web-motion
description: Create premium cinematic web experiences with scroll-driven storytelling, sophisticated motion design, 3D scenes, camera movement, video scrubbing, frame-by-frame scroll scrubbing, AI-generated video pipelines, subject isolation, kinetic typography and micro-interactions. Use when building or redesigning websites that should feel cinematic, immersive, premium and visually distinctive, especially landing pages and brand experiences.
---

# Cinematic Web Motion

## Purpose

Create high-end web experiences where motion communicates the brand, story and value proposition.

The result should feel directed rather than decorated. Scrolling should control a visual narrative, like a film whose timeline the visitor controls.

Core principle:

**Story first. Technology second. Performance always.**

Do not start by choosing Three.js, GSAP or another library. First understand the business, audience, content, conversion goal and available assets. Then choose the simplest technology capable of producing the intended effect.

## When to use this skill

Use this skill when the task involves one or more of:

- cinematic landing pages
- scroll-driven storytelling
- premium website motion
- 3D web scenes
- camera movement
- video controlled by scroll
- frame-by-frame scroll animation
- immersive hero sections
- sophisticated page transitions and section handoffs
- visual storytelling for brands
- high-end automotive, architecture, technology, product or service websites
- redesigns where the existing site needs a more distinctive visual experience
- AI-generated video or imagery turned into a frame-by-frame scroll animation
- subject isolation (character, product, vehicle separated from its background)
- kinetic typography / text motion
- magnetic buttons, cursor interactions and other high-quality micro-interactions

Do not force this skill onto ordinary dashboards, documentation, simple CRUD applications or content-heavy sites where cinematic motion would reduce usability.

## Required workflow

Before implementing substantial motion:

1. Inspect the existing project.
2. Inspect the existing website if a URL is available.
3. Understand the business and target audience.
4. Identify the primary conversion action.
5. Inspect existing branding, logo, typography, colors, imagery and content.
6. Identify existing routes and URLs that should be preserved.
7. Determine what assets already exist and what assets are missing.
8. Design the story before implementing animation.
9. Select the least complex suitable animation technology.
10. Implement the cinematic section.
11. Connect the cinematic section to normal semantic HTML content.
12. Test desktop, tablet and mobile behavior.
13. Test reduced-motion behavior.
14. Optimize loading and runtime performance.
15. Verify that SEO content is real HTML and not trapped inside Canvas, WebGL or video.

Never destroy or replace existing project content before understanding it.

Never invent customer logos, statistics, certifications, awards, partner counts, locations, reviews or business claims.

## Story design

Think in scenes, not sections.

A cinematic sequence should usually contain:

1. Establish
2. Movement
3. Disruption
4. Freeze or transformation
5. Reveal
6. Scale
7. Resolution
8. Conversion

The exact structure can change depending on the business.

### Example pattern

A vehicle website might use:

Vehicle moving → vehicle stops → environment freezes → service takes control → camera pulls out → nationwide network appears → camera returns → help arrives → journey continues → CTA.

A technology company might use:

Product object appears → camera approaches → internal mechanism is revealed → system expands into a network → key benefit appears → product returns to normal scale → CTA.

The narrative should communicate something meaningful about the company.

## Motion hierarchy

Do not animate everything.

Prioritize:

1. Hero/story motion
2. Primary visual object
3. Camera movement
4. Major transitions
5. Key content reveals
6. Secondary micro-interactions

Avoid animating every card, word and icon independently.

Motion should create hierarchy rather than visual noise.

## Camera principles

When 3D or cinematic imagery is used, camera movement should have a reason.

Useful movements:

- tracking shot
- dolly in
- dolly out
- orbit
- controlled pan
- pullback
- reveal through depth
- parallax
- focus-like depth transition

Avoid random camera movement.

The visitor should feel that the camera is intentionally directed.

## Scroll as a timeline

Treat scroll progress as a normalized timeline:

`0.0 → beginning`
`0.25 → scene transition`
`0.5 → central reveal`
`0.75 → scale/change`
`1.0 → final state`

Animation should be deterministic from scroll progress whenever possible.

Do not build important cinematic effects around arbitrary scroll event callbacks that produce inconsistent timing.

Use requestAnimationFrame, a timeline library or another controlled animation loop.

## Animation mapping

For any section more complex than a simple fade-in, write the progress-to-state mapping down before implementing. Example:

```text
0.00  hero visible, subject at rest
0.15  supporting text begins to fade out
0.30  subject begins moving
0.50  subject reaches the midpoint of the frame
0.70  background transitions
0.85  next section's text starts appearing
1.00  handoff to next section complete
```

This mapping is what makes scroll-scrubbed frame sequences, GSAP timelines and section handoffs consistent with each other — every technology in the section should be reading from the same progress value and the same mapping, not from independent, uncoordinated triggers.

## Visual hierarchy

For every animated section, be able to answer:

1. What should the visitor see first?
2. What is moving, specifically?
3. Why is it moving — what does the motion communicate?
4. What should the visitor discover as they keep scrolling?
5. What is the next visual state?
6. Where does the animation end, and what happens at that boundary?

If you cannot answer "why is it moving," reconsider whether it should move at all. Do not animate everything in a section simultaneously — see "Motion hierarchy" above.

## Technology selection

Choose the simplest suitable implementation.

### CSS

Use CSS for:

- hover states
- simple fades
- transforms
- basic transitions
- small UI motion

### Framer Motion

Prefer Framer Motion when working in React and the need is:

- entrance/exit animations
- layout transitions and shared-layout ("magic move") transitions between states or routes
- simple scroll-linked transforms (e.g. `useScroll`/`useTransform`-style progress mapping)
- hover/tap/drag micro-interactions expressed declaratively alongside components
- UI motion that should stay tightly coupled to component state

Framer Motion and GSAP are not mutually exclusive on the same page — it's reasonable to use Framer Motion for UI-level motion and GSAP for a complex pinned cinematic timeline elsewhere on the same site. Avoid using both for the same effect.

### GSAP + ScrollTrigger

Use GSAP when the experience needs:

- scroll timelines
- pinning
- scrubbing
- sequencing
- synchronized transforms
- complex reveal timing
- camera/value interpolation

Prefer timeline-based animation over many unrelated event handlers.

### Video scrubbing

Use HTML video when:

- the cinematic sequence already exists as video
- realistic motion is more important than per-frame procedural control
- a generated or filmed sequence is available

The scroll position should map to video time.

Provide a poster/fallback while the video is loading.

Do not make the website unusable while waiting for the video.

### Canvas + frame sequence

Use Canvas when:

- exact frame control is required
- a cinematic sequence should be tied tightly to scroll
- the source is a rendered image sequence
- video seeking would be too inconsistent

Use modern image formats such as WebP or AVIF where practical.

Load frames progressively rather than downloading a huge sequence immediately.

Decide the frame count and the scroll distance together before any source video is produced or extracted — see `references/image-sequences.md` for the planning method and the exact scroll-progress-to-frame-index formula.

### SVG

Use SVG for:

- logos
- icons
- line/path drawing (stroke-dashoffset reveals)
- simple illustrative shapes and morphs

SVG animation is cheap and crisp at any resolution, and is usually the right choice before reaching for Canvas or a heavier library for anything logo/icon/line-based.

### Three.js

Use Three.js only when actual 3D is necessary.

Good reasons:

- real 3D geometry
- camera movement
- lighting
- depth
- object interaction
- procedural scenes
- 3D transformations that cannot reasonably be faked

Do not use Three.js just to create a rotating cube or decorative WebGL background.

Keep geometry, textures, lights and shaders as lightweight as possible.

## Architecture

Prefer a replaceable cinematic renderer architecture.

Conceptually:

`CinematicSection`
→ `ScrollController`
→ `AnimationTimeline`
→ `Renderer`
→ `ProgressMapping`
→ `OverlayContent`

The renderer can be:

- video
- canvas frame sequence
- Three.js
- CSS
- another appropriate implementation

The story should not depend unnecessarily on one renderer.

This makes it possible to replace a temporary generated video with a final production asset later.

## Video and frame-sequence replacement

Build cinematic sections so that temporary assets can be replaced without rewriting the entire page.

For example:

- temporary MP4 → final MP4
- temporary GIF → optimized video
- placeholder images → AVIF/WebP frame sequence
- procedural Three.js scene → production 3D asset

Do not hard-code business logic into the media renderer.

## Subject isolation

When a scene centers on a character, product, vehicle or other focal object, check whether that subject should be isolated from its background rather than treated as one flat scene:

```text
Layer 1  Background
Layer 2  Typography
Layer 3  Subject (character / product / vehicle)
Layer 4  Decorative elements
```

An isolated subject can be animated, scaled, pinned and handed off between sections independently of its background. Prefer isolating the subject before animating it, especially when the subject originates from generated video — see `references/ai-video-pipeline.md`.

## AI-generated video and image assets

When a cinematic section needs a visual asset that does not already exist, use the project's KIE Creative MCP for image and video generation rather than defaulting to stock imagery or skipping the visual entirely.

An AI-generated video is not automatically a `<video>` element. It is frequently raw material for a scroll-scrubbed frame sequence:

```text
AI video → KIE Creative MCP → rendered video
  → frames extracted → WebP/AVIF sequence
  → scroll position selects frame → frame is rendered
```

The result is an interactive, scroll-controlled experience, not passive video playback.

Prefer this end-to-end order for a scroll-scrubbed animated subject:

1. define the visual concept
2. analyze any design reference supplied
3. determine the UI layout and text position (headline, subtext, CTA) before writing any prompt
4. generate a key visual (still), composed around the reserved UI-safe area
5. isolate the subject
6. write a full, production-grade video prompt (never a one-line description) — see below
7. generate video via the KIE Creative MCP, producing multiple deliberately different variants for hero/scroll-critical sequences
8. select the best variant against the actual website composition, not in isolation
9. conform the video to the needed frame rate
10. extract exactly the planned number of frames
11. optimize frames for the web
12. implement scroll-scrubbing
13. implement pinning
14. implement the web/UI overlay in the reserved UI-safe area
15. implement the section handoff
16. implement a mobile fallback
17. test performance

Do not generate an arbitrary video and then try to force the animation or the text overlay to fit it afterward — the frame count, scroll distance, motion pacing and UI-safe area must be planned before generation, and the generated footage is chosen/regenerated to match that plan. Full detail in `references/ai-video-pipeline.md`.

### Video prompt engineering

The prompt handed to the video model is a first-class design artifact, not an afterthought. A prompt for a web-bound video must specify subject, starting position, action, body mechanics, camera behavior, composition, lighting, environment, temporal progression (start → motion → end state) and — critically — which regions of the frame must stay visually clean for the planned text/CTA overlay.

Hard rule: never let the video model render UI text, headlines, buttons or logos into the footage. The video is the visual layer only; real text is layered on top afterward as HTML/CSS. Write the prompt so composition and motion naturally leave the planned text area clean, rather than depending on the model to draw the text and then cropping it out.

Do not wait for the user to say "leave room for the text." If the layout implies text or UI will sit over the video, work out the UI-safe area and encode it into the prompt automatically, before generating anything.

Full prompt structure, camera vocabulary, negative-constraint guidance, use-case profiles (cinematic hero, scroll-scrub character, product showcase, section transition, background animation) and variant-selection criteria are in `references/video-prompt-engineering.md` — read it before writing any prompt for a web-bound AI video.

## Transitions

Prefer physical or conceptual transitions.

Strong examples:

- local scene → national map
- object → system
- vehicle → network
- close-up → wide establishing shot
- stillness → movement
- darkness → reveal
- individual problem → coordinated solution

Weak examples:

- random zoom
- random blur
- arbitrary particle explosion
- unrelated 3D objects
- excessive neon
- generic SaaS blobs

## Section handoffs

Prefer a handoff over a hard cut whenever two adjacent sections share a visual or narrative relationship: a subject that continues moving from one section into the next, a headline that hands off to the next section's headline, or a background that morphs rather than switches. Plan what crosses the section boundary, in what state it arrives, and where it settles, as part of the animation mapping — not after both sections are already built independently. A hard cut is fine when sections are genuinely unrelated. See `references/transitions.md` for handoff patterns.

## Typography motion

Text is a designed, animatable element — not just content that fades in by default. Useful techniques include character/word/line reveals, masked or clip-path reveals, scroll-bound split text, blur-to-sharp focus, scroll-based scale/opacity, and variable-font weight animation. Match the technique to its narrative beat: a hero statement can justify a one-time reveal; a scroll-scrubbed section should bind text state to the same progress value as the rest of the scene. Never character-stagger long-form body copy, and never let animated text fall out of the accessibility tree. Full guidance in `references/typography-motion.md`.

## Micro-interactions

Small interface-level motion — buttons, links, cards, navigation, cursor-reactive elements — should feel intentional and subtle, not flashy. Useful patterns: magnetic pull toward the cursor within a small radius, subtle scale on hover, underline reveals, icon nudges, cursor-following elements with slight lag. Restrict cursor-following and magnetic effects to devices with real pointer input, always provide an equivalent `:focus-visible` state for keyboard users, and keep the interaction responsive even mid-animation. Full guidance in `references/micro-interactions.md`.

## Design direction

The visual language should normally be:

- premium
- restrained
- intentional
- modern
- cinematic
- brand-specific

Avoid:

- generic AI landing page aesthetics
- excessive gradients
- fake terminal windows
- fake computer screens
- random dashboards
- unnecessary glassmorphism
- excessive neon
- excessive particles
- generic stock imagery
- cheesy industry clichés

If the brand is traditional, do not make it look like a futuristic gaming site just because 3D is available.

## Content integration

Cinematic motion is not the entire website.

After the story, explain:

- what the company does
- who it serves
- why it is different
- important services
- proof/trust
- the next action

The cinematic experience should lead naturally into useful content.

Do not hide essential information behind animation.

## Conversion

The cinematic story should support conversion.

A common sequence is:

`Story`
→ `Problem`
→ `Solution`
→ `Trust`
→ `Service`
→ `CTA`

The primary CTA should remain understandable even if animation is disabled.

Use clear calls to action such as:

- Anfrage senden
- Termin vereinbaren
- Kontakt aufnehmen
- Angebot anfragen
- Partner werden

Choose wording based on the actual business.

## SEO

Cinematic content must not replace semantic HTML.

Use:

- one meaningful H1
- logical H2/H3 hierarchy
- descriptive text
- semantic sections
- descriptive links
- alt text for meaningful images
- canonical URLs
- metadata
- Open Graph metadata
- robots.txt
- sitemap.xml
- structured data where appropriate
- hreflang for multilingual sites
- clean URLs

Important information must not exist only inside:

- Canvas
- WebGL
- video
- generated images

The crawler and user should still receive the business information as HTML.

## Accessibility

Always account for:

- `prefers-reduced-motion`
- keyboard navigation
- readable contrast
- focus states
- semantic HTML
- meaningful alternative text
- controls that remain usable without animation

For reduced motion:

- disable or simplify cinematic scrubbing
- remove unnecessary camera movement
- shorten transitions
- keep content visible
- never hide essential information because motion was disabled

## Mobile strategy

Do not simply shrink the desktop animation.

Mobile has:

- less screen space
- different scroll behavior
- less GPU headroom
- different aspect ratios
- potentially weaker networks

Create a dedicated mobile strategy.

Possible changes:

- shorter sequence
- fewer frames
- reduced 3D complexity
- simplified camera movement
- static poster
- fewer particles
- lower resolution assets
- alternative composition

The mobile version should still feel intentional and premium.

## Performance

Performance is part of the design.

Prefer:

- GPU-friendly transforms
- opacity
- efficient canvas rendering
- compressed media
- responsive image sizes
- lazy loading
- progressive loading
- nearby-frame preloading
- caching
- code splitting where useful
- cleanup of animation listeners
- disposal of Three.js resources

Avoid repeatedly animating:

- width
- height
- top
- left

when transforms can achieve the same result.

Avoid huge uncompressed videos and image sequences.

Do not load a large cinematic asset before the user can benefit from it unless there is a strong reason.

## Loading behavior

Every cinematic section should have a graceful loading state.

Possible strategy:

1. show poster/fallback
2. load critical assets
3. begin cinematic experience
4. progressively load additional frames/assets
5. continue normal page rendering independently

Never block the complete website behind a cinematic asset.

## Asset quality

If using generated media:

- prefer realistic motion
- avoid visible AI artifacts
- avoid text rendered inside generated imagery
- avoid logos generated by image/video models
- add actual logo/text as HTML/SVG
- maintain visual continuity between scenes
- keep camera direction consistent

For generated video, favor continuous shots and transitions over rapid cuts when the video will be scrubbed by scroll.

## 3D scene principles

A good web 3D scene generally has:

- one clear subject
- controlled lighting
- intentional camera
- limited geometry
- strong composition
- restrained materials
- meaningful depth

Do not fill the screen with unrelated objects.

For product scenes, prioritize silhouette and readability over technical complexity.

For environments, use depth and atmosphere carefully.

## Failure modes

Avoid these common mistakes:

### Technology-first development

Bad:

"Let's use Three.js because the page needs to look cool."

Good:

"The story requires a real 3D camera move, therefore Three.js is justified."

### Animation everywhere

Bad:

Every section fades, slides and rotates.

Good:

One major cinematic sequence establishes the experience, while the rest of the page uses restrained motion.

### No fallback

Bad:

The entire hero is blank until a 40 MB video loads.

Good:

A poster and semantic HTML exist immediately.

### Cinematic but meaningless

Bad:

Beautiful animation that never explains the business.

Good:

Every major visual transition communicates something about the product, service or brand.

### Generic 3D

Bad:

Floating spheres and glowing lines for every company.

Good:

The 3D visual language is derived from the actual business.

## Debugging discipline

Scroll-driven cinematic code fails in ways that are easy to visually paper over rather than actually fix, particularly around pinning, ScrollTrigger configuration, z-index, overflow, sticky positioning, transforms, viewport height, responsive breakpoints, hydration, and animation state.

When a quick change makes a bug appear to go away, check whether it addressed the actual cause or only hid the symptom. "The section looks right again" is not the same claim as "the bug is fixed." Examples of the difference:

- Adding `overflow: hidden` to stop a stray scrollbar without finding which element is overflowing — the underlying layout bug remains and will resurface elsewhere.
- Increasing `end` on a ScrollTrigger until pinning "feels" right without understanding why the original value produced the wrong pin duration.
- Wrapping a hydration mismatch in a client-only render without understanding why server and client markup diverged.
- Adjusting a `z-index` until an element appears on top without understanding why the stacking context put it underneath in the first place.

Before moving on from a fix, be able to state why the original code was wrong — not just that the new code visually resolves it.

## Project documentation

If the project does not yet have a CLAUDE.md and the work involves a non-trivial cinematic build, create one before making large-scale changes. Document:

- tech stack
- animation architecture (which sections use CSS, Framer Motion, GSAP, Canvas, SVG, Three.js, and why)
- libraries in use
- asset strategy (image/video formats, generation source)
- frame strategy (frame counts, resolutions, loading strategy per sequence)
- responsive/mobile strategy
- design rules specific to the project
- performance rules specific to the project

This keeps later prompts and later sessions consistent with decisions already made, instead of re-deriving or contradicting them.

## Implementation checklist

Before declaring the cinematic implementation complete, verify:

- [ ] Existing site/project was inspected first
- [ ] Business story is clear
- [ ] Primary CTA is clear
- [ ] Animation technology is justified
- [ ] Main cinematic sequence has a beginning, transformation and resolution
- [ ] Motion is tied to scroll progress where appropriate
- [ ] Essential content exists as semantic HTML
- [ ] Desktop works
- [ ] Mobile works
- [ ] Reduced motion works
- [ ] Keyboard/accessibility basics work
- [ ] Loading state exists
- [ ] Large assets are optimized
- [ ] Three.js resources are disposed when needed
- [ ] No invented business claims
- [ ] Existing useful URLs/content are preserved where possible
- [ ] SEO metadata is implemented
- [ ] The cinematic section leads naturally to useful content and CTA
- [ ] Frame count and scroll distance for any frame sequence were planned together, not fitted after the fact
- [ ] Subject isolation was considered when a focal character/product/vehicle is animated
- [ ] Any AI-generated video/image asset was produced for this specific sequence, not repurposed unrelated footage
- [ ] The video prompt was written with the UI layout/text position decided first, and reserves a clean UI-safe area
- [ ] No UI text, headlines, buttons or logos were rendered by the video model itself
- [ ] Section handoffs were planned deliberately where a visual/narrative relationship exists between adjacent sections
- [ ] Kinetic typography respects reading speed and remains in the accessibility tree
- [ ] Micro-interactions have keyboard-focus equivalents and are disabled on touch where cursor-only
- [ ] Any apparent bug fix addresses a root cause, not just a visual symptom
- [ ] A CLAUDE.md documents the animation architecture, if this is a substantial build

## References

Read the relevant reference files before implementing complex work:

- `references/story-design.md` for cinematic narrative design
- `references/scroll-animation.md` for scroll/timeline architecture
- `references/gsap-scrolltrigger.md` for GSAP implementation patterns
- `references/threejs.md` for 3D scene architecture
- `references/video-scrubbing.md` for scroll-controlled video
- `references/image-sequences.md` for Canvas frame sequences and the frame-by-frame scroll-scrubbing formula
- `references/ai-video-pipeline.md` for the KIE Creative MCP workflow, subject isolation and AI-video-to-frame-sequence production
- `references/video-prompt-engineering.md` for writing production-grade, UI-aware prompts for web-bound AI video
- `references/typography-motion.md` for kinetic typography techniques
- `references/micro-interactions.md` for magnetic buttons, cursor interactions and hover motion
- `references/transitions.md` for visual transition design and section handoffs
- `references/performance.md` for optimization
- `references/mobile.md` for mobile-specific strategy
- `references/accessibility.md` for reduced motion and accessible animation

Use only the references relevant to the task instead of loading everything unnecessarily.
