# Scroll-Controlled Video

## When to use

Use video scrubbing when a realistic cinematic sequence already exists.

This is often preferable to recreating a real-world scene with WebGL.

## Basic model

Map scroll progress to video time:

`video.currentTime = progress * video.duration`

Use requestAnimationFrame or a controlled animation mechanism rather than writing to currentTime for every raw scroll event.

## Video requirements

Prefer:

- short sequences
- efficient codecs
- reasonable resolution
- correct aspect ratios
- poster image
- compressed file size
- continuous shots where possible

For a scroll-controlled cinematic sequence, rapid cuts can feel confusing because the visitor can move backward and forward through the timeline.

## Loading

Show a poster while metadata/media loads.

Do not make the complete page dependent on the video.

## Mobile

Possible mobile alternatives:

- lower-resolution video
- shorter sequence
- different crop
- simplified animation
- static poster with subtle CSS motion

## Generated video

If AI-generated footage is used:

- avoid generated text
- avoid generated logos
- keep brand elements in HTML/SVG
- check continuity frame by frame
- verify that the main object does not morph
- avoid excessive camera changes

## GIF warning

GIF is generally a poor final format for cinematic web motion because of:

- large file size
- limited compression
- limited color efficiency
- weak seeking/control
- poor mobile performance

Use video or optimized frame sequences instead.
