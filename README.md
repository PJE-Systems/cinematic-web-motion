# cinematic-web-motion

A Claude Code / Claude Agent skill for building **premium, cinematic web experiences** — websites that feel like directed digital experiences instead of static pages with a few animations bolted on.

> **Story first. Technology second. Performance always.**

## What this skill does

`cinematic-web-motion` teaches Claude to design and implement scroll-driven storytelling, sophisticated motion design, and AI-generated video pipelines the way a high-end digital agency would — with a clear narrative reason behind every animation, not motion for its own sake.

It covers the full range of modern web motion:

- **Scroll-driven animation** — scroll scrubbing, pinning, section handoffs, viewport-based reveals
- **Frame-by-frame scroll scrubbing** — scroll position deterministically selects the visible frame, with a planned frame-count/scroll-distance formula
- **AI-generated video pipelines** — using the project's KIE Creative MCP to generate video assets, then turning them into scroll-controlled frame sequences instead of passive `<video>` playback
- **Professional video prompt engineering** — production-grade, UI-aware prompts (subject, camera, composition, lighting, temporal progression, UI-safe areas) so AI video composes cleanly with real HTML text and CTAs
- **Subject isolation** — separating a character, product or vehicle from its background so it can be animated, scaled, pinned and handed off independently
- **Section handoffs** — elements that visually survive the boundary between sections instead of hard-cutting
- **Kinetic typography** — character/word/line reveals, masked text, scroll-bound text, variable font animation
- **Micro-interactions** — magnetic buttons, cursor interactions, hover states, subtle premium UI motion
- **3D scenes and camera work** (Three.js) — with intentional camera language, not decorative WebGL
- **Technology selection** — CSS, Framer Motion, GSAP + ScrollTrigger, Canvas, SVG, Three.js, chosen by the problem, not by default

Every technique is paired with explicit performance, mobile, accessibility (`prefers-reduced-motion`) and SEO guardrails, so cinematic motion never comes at the cost of usability, crawlability or load time.

## Why this skill exists

AI-assisted website builds tend to converge on the same generic patterns: fade-in-on-scroll everywhere, decorative WebGL blobs, autoplaying videos with no purpose, and text baked into AI-generated footage. This skill pushes in the opposite direction:

- **Design-first, not technology-first.** Understand the business, audience and story before picking a library.
- **Motion has to justify itself.** Every animated element must answer "why is it moving?" — not just "can it move?"
- **AI-generated assets are design assets, not shortcuts.** A video generated for a hero section is planned around the UI layout — text position, CTA placement, UI-safe areas — *before* the generation prompt is written, never fitted onto the footage afterward.
- **Root-cause debugging.** A pinning/z-index/overflow fix that makes a bug "look" resolved isn't accepted as fixed until the actual cause is understood.

## Structure

```
cinematic-web-motion/
├── SKILL.md                          Core principles, workflow, technology selection, checklists
├── examples/
│   └── cinematic-landing-page.md     Worked example
└── references/
    ├── story-design.md               Cinematic narrative design (scenes, motion hierarchy, camera principles)
    ├── scroll-animation.md           Scroll-as-timeline architecture, pinning, scrubbing, cleanup
    ├── gsap-scrolltrigger.md         GSAP + ScrollTrigger implementation patterns
    ├── threejs.md                    3D scene architecture and camera work
    ├── video-scrubbing.md            Scroll-controlled HTML video
    ├── image-sequences.md            Canvas frame sequences, frame-mapping formula, loading strategies
    ├── ai-video-pipeline.md          End-to-end AI video → frame sequence production pipeline
    ├── video-prompt-engineering.md   Writing production-grade, UI-aware prompts for AI video generation
    ├── typography-motion.md          Kinetic typography techniques
    ├── micro-interactions.md         Magnetic buttons, cursor interactions, hover motion
    ├── transitions.md                Visual transition design and section handoffs
    ├── performance.md                Asset, memory and runtime performance rules
    ├── mobile.md                     Mobile-specific animation strategy
    └── accessibility.md              Reduced motion and accessible animation
```

`SKILL.md` is the entry point Claude reads first; the reference files are loaded selectively, only when the task actually needs that depth.

## When Claude reaches for this skill

- cinematic landing pages and premium brand experiences
- scroll-driven storytelling and pinned/scrubbed hero sections
- AI-generated video or imagery turned into a scroll animation
- subject isolation (a character, product or vehicle as its own animated layer)
- kinetic typography and text motion
- magnetic buttons, cursor interactions and other high-end micro-interactions
- 3D web scenes with real camera movement
- redesigns where an existing site needs a more distinctive visual experience

It intentionally stays out of the way for dashboards, documentation, plain CRUD apps and content-heavy sites where cinematic motion would hurt usability more than it helps.

## AI video pipeline at a glance

```
Reference → Creative direction → UI layout / text position → Key visual
  → Subject isolation → Video prompt → AI video (KIE Creative MCP)
  → Variant selection → Frame extraction → Scroll scrubbing → Pinning
  → Web/UI overlay → Section handoff → Mobile fallback → Performance
```

The UI layout is decided **before** the video prompt is written — the prompt explicitly reserves clean, low-contrast regions for the headline, subtext and CTA that will later be overlaid as real HTML/CSS. The video model is never asked to render UI text, logos or captions into the footage.

## Requirements

- A project with access to the **KIE Creative MCP** (`pje-creative`) for AI image/video generation, when the AI-asset pipeline is used. The rest of the skill (scroll animation, GSAP, Three.js, typography, micro-interactions) has no MCP dependency and works with any modern web stack.
- Project-side libraries are chosen per task, not bundled by the skill — typically some combination of `gsap` (with the ScrollTrigger plugin), `framer-motion`, and/or `three`, only when the chosen technique actually needs them.

## Installation

Drop the `cinematic-web-motion/` directory into your skills directory (e.g. `~/.claude/skills/`) so `SKILL.md` is discoverable. No build step or dependency installation is required for the skill itself.

