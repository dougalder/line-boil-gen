# Changelog

All notable changes to Line Boil Generator are documented in this file.

## [1.11] – October 2024

### Added
- **Select Tool**: Click layers directly in the preview canvas to select them
- **Improved Layer Picking**: Text layers can be clicked anywhere in their bounding box; artwork responds to per-pixel alpha
- **Gizmo Priority**: Layer handles are properly z-ordered and don't block selection of layers beneath

### Fixed
- Layer selection now works smoothly with the floating toolbar
- Handle overlay no longer swallows pointer events for layers underneath

---

## [1.10] – October 2024

### Fixed
- **Canvas Resize Flicker**: Fixed major issue where dragging to resize a layer caused the canvas to flicker between old and new sizes
- The problem was traced to the playback rAF loop overpainting the pre-drag frames; now `state.dragging` prevents repaints during manipulation
- Resize is now smooth from start to finish

---

## [1.9] – October 2024

### Added
- **Text Layer Enhancements**: Text gizmos now show bounds correctly using `actualBoundingBox*` metrics instead of em padding
- Text resize handle is now positioned relative to actual ink, not padding
- Text box measurements are more accurate, making the resize ratio less surprising

### Fixed
- Text box measured from em padding (~2.7× letter height) – now measures real ink with `actualBoundingBox*`
- Composite canvas was locked to source image size; now uses union canvas with `workOffset`
- Text pushed past edges can now resize within the full workspace bounds

---

## [1.8] – October 2024

### Added
- **Fixed Workspace Frame**: The document bounds are now fixed at `state.doc.w/h` instead of the union of visible layers
- This fixes the old behavior where the canvas would shrink when layers were scaled or moved
- "Fit to content" is now an optional button that repositions layers rather than changing the frame

- **Trim Baked at Import**: Trim is applied once at import (with `TRIM_MARGIN = 20px`) instead of every render
- "Trim to artwork" in Output tab is opt-in and defaults to **off**

- **Floating Toolbar**: Toolbar now floats over the preview with 13 buttons:
  - Select, Import, Paste, Text, Duplicate, Delete
  - Undo, Redo, Play/Pause, Reroll, Boil, Cycle, Export
- Toolbar collapses to a static bar on screens narrower than 620px
- Boil button opens a popover that drives the Boil tab's controls (single source of truth)

### Fixed
- Canvas no longer chases artwork when layers are scaled or moved
- Workspace is now stable and predictable

---

## [1.7] – October 2024

### Added
- **Layer System**: Ordered stack of image and text layers
  - Each layer can be hidden, moved, resized, rotated, and deleted
  - Layers are composited into a single flattened canvas before boiling
  - Layer rasterization is cached using a content signature
  
- **Per-Layer Drop Shadow**: Each layer can have an optional drop shadow with adjustable offset and blur
  
- **Undo/Redo**: 40-level history with automatic coalescing
  - Keyboard shortcuts: Cmd/Ctrl+Z (undo), Cmd/Ctrl+Shift+Z (redo)
  - Changes to the same property within a short time window are coalesced into a single undo step
  
- **Layer Handles**: Interactive on-screen controls for resize, move, and rotate
  - Corner handles for scaling
  - Side handles for moving
  - Top-center handle for rotation
  
- **Layer Properties Panel**: Edit layer name, opacity, and effects without modal dialogs

### Design
- All downstream code still boils a single flattened canvas, keeping the architecture safe

---

## [1.6] – October 2024

### Added
- **Version Badge**: Displays app version in the interface
- **Favicon**: Custom SVG favicon matching the app branding
- **"How this works" Panel**: Informational overlay explaining the app features
- **20px Trim Margin**: Images are automatically trimmed with 20-pixel margin preserved
- **Larger Touch Sliders**: Sliders are automatically enlarged on touch devices (80px height vs 40px)
- **Manual Touch Toggle**: Override automatic detection if needed
- **Clear × Fields**: Input fields have × button to clear quickly
- **Toggle to Hide Tab Panel**: Collapse the right panel for more preview space
- **Demo Restore Button**: Reload the demo image at any time
- **Import/Paste Progress**: Visual feedback while processing large images

### Fixed
- **iPad Stretching**: Fixed aspect ratio distortion on iPad by deriving both canvas dimensions from a single scale factor
  - Previously used `max-width` + `max-height` together, which caused Safari to stretch
  - Now derives height from width (or vice versa) for consistent ratio across all viewports

---

## [1.5] – October 2024

### Added
- **Text Support**: Add text to animations with customizable fonts and sizes
- **Font Selection**: Multiple typefaces including sans-serif, serif, monospace, and display fonts
- **Text Color**: Fill and outline colors with independent selection
- **Text Positioning**: Move and resize text layers with on-screen handles

### Fixed
- **iOS Font Loading**: Fonts weren't loading in Safari on iOS because canvas alone doesn't trigger font download
  - Fixed with off-screen probe nodes and measurement-based detection

---

## [1.4] – October 2024

### Added
- **Background Removal**: Automatic alpha extraction from solid-color backgrounds
- **Flood Fill**: Smart flood fill with smoothstep fringe detection
- **Transparency Preview**: Checkerboard background for transparency visualization

---

## [1.3] – October 2024

### Added
- **Crop Tool**: Define a custom crop region
- **Auto-Crop on Export**: Optional crop bounding box in Output tab

---

## [1.2] – October 2024

### Added
- **Output Tab Controls**: Length and frame-rate sliders
- **File Size Estimates**: Estimated file sizes for GIF, APNG, MP4, and WebM
- **Processing Feedback**: Status messages during long encodes
- **Responsive Tab Layout**: Tabs stay above the fold on most screens

---

## [1.1] – October 2024

### Added
- **MP4 Export**: H.264 video export (fixed MediaRecorder returning VP9)
- **WebM Export**: VP9 video export via MediaRecorder
- **Green-Screen Video**: Transparent background option for video exports
- **Custom MP4 Muxer**: ISO-BMFF writer for direct H.264 encoding
- **File Size Optimization**: Selectable quality/size tradeoffs for video

### Fixed
- **MediaRecorder VP9 Bug**: Browser was returning VP9-in-MP4 instead of H.264; now uses WebCodecs H.264 with custom ISO-BMFF muxer

---

## [1.0] – September 2024

### Initial Release
- **GIF Export**: Hand-written LZW encoder with median-cut palette and transparency
- **APNG Export**: Custom APNG builder with frame control
- **PNG Sequences**: Export individual frames as ZIP-compressed PNG files
- **Six Effects**: Jitter, Warp, Ripple, Tremble, Swell, Drift
- **Variations**: Generate 1–12 different animation cycles
- **Responsive Design**: Desktop, tablet, and mobile layouts
- **Offline**: Works without network after initial load (Google Fonts only)
- **Zero Dependencies**: Pure JavaScript, no frameworks or libraries

---

## Technical Notes

### Encoding Performance
- GIF: ~100–500ms (depends on palette complexity)
- APNG: ~50–300ms
- MP4: ~500–2000ms (WebCodecs hardware acceleration when available)
- PNG Frames: ~50–200ms per frame
- WebM: Variable (MediaRecorder dependent)

### Browser Requirements
- Canvas 2D with ImageData
- Web Workers (for parallel processing)
- WebCodecs API (for H.264; WebM fallback available)
- FileReader API
- Blob API

---

**[1.11]**: https://github.com/user/line-boil-gen/releases/tag/v1.11
