---
name: cinematic-web-motion
description: Create premium cinematic web experiences with scroll-driven storytelling, sophisticated motion design, 3D scenes, camera movement, video scrubbing and frame sequences. Use when building or redesigning websites that should feel cinematic, immersive, premium and visually distinctive, especially landing pages and brand experiences.
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
- sophisticated page transitions
- visual storytelling for brands
- high-end automotive, architecture, technology, product or service websites
- redesigns where the existing site needs a more distinctive visual experience

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

## Technology selection

Choose the simplest suitable implementation.

### CSS

Use CSS for:

- hover states
- simple fades
- transforms
- basic transitions
- small UI motion

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

## References

Read the relevant reference files before implementing complex work:

- `references/story-design.md` for cinematic narrative design
- `references/scroll-animation.md` for scroll/timeline architecture
- `references/gsap-scrolltrigger.md` for GSAP implementation patterns
- `references/threejs.md` for 3D scene architecture
- `references/video-scrubbing.md` for scroll-controlled video
- `references/image-sequences.md` for Canvas frame sequences
- `references/transitions.md` for visual transition design
- `references/performance.md` for optimization
- `references/mobile.md` for mobile-specific strategy
- `references/accessibility.md` for reduced motion and accessible animation

Use only the references relevant to the task instead of loading everything unnecessarily.
