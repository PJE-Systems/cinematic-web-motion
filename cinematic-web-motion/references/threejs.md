# Three.js for Cinematic Web Experiences

## Use Three.js when

The visual genuinely needs:

- 3D geometry
- real camera movement
- depth
- lighting
- 3D interaction
- procedural environments
- controlled object transformations

## Scene hierarchy

Prefer a simple hierarchy:

```text
Scene
├── Environment
├── Main Subject
├── Secondary Elements
├── Lights
└── Camera
```

Keep the main subject visually dominant.

## Camera

Use camera movement as storytelling.

Examples:

- close-up → wide shot reveals scale
- side tracking → establishes motion
- orbit → reveals object
- pullback → reveals network/system

Avoid constant camera movement.

## Lighting

Use a small number of purposeful lights.

Avoid turning every scene into a glowing sci-fi environment.

## Geometry

Prefer:

- low/moderate polygon counts
- instancing where appropriate
- compressed textures
- reused materials
- baked details when possible

## Assets

If importing 3D models:

- optimize geometry
- compress textures
- use appropriate texture resolution
- lazy-load noncritical assets
- dispose resources when the scene is destroyed

## Mobile

On smaller devices consider:

- lower pixel ratio
- fewer objects
- simpler materials
- fewer lights
- lower texture resolution
- reduced animation complexity
- static fallback if necessary

Never assume a desktop GPU can be replicated on mobile.

## React integration

Keep the render loop outside React state updates.

Use refs and imperative rendering for high-frequency operations.

Do not set React state on every frame unless there is a very specific reason.
