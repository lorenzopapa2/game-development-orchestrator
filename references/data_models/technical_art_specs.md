# Technical Art Specifications

Hard technical constraints for art production across platforms and engines. When generating art specs, asset lists, or outsourcing briefs, you MUST apply the platform-appropriate limits from this file. Art that exceeds these limits will cause performance failures in the target platform.

For design methodology and art pipeline workflows, see [../art-animation.md](../art-animation.md).
For image generation tool routing, see [../image-generation.md](../image-generation.md).

## 1. Platform Performance Budgets

### Mobile (iOS/Android)

| Parameter | Low-End Target | Mid-Range Target | High-End Target |
|-----------|---------------|-----------------|----------------|
| Target FPS | 30 | 30-60 | 60 |
| Draw calls per frame | <100 | <200 | <500 |
| Triangle count per frame | <100K | <300K | <750K |
| Texture memory | <256MB | <512MB | <1GB |
| Total app size | <200MB (ideal), <500MB (max without expansion) | <1GB | <2GB |
| RAM usage | <1GB | <2GB | <3GB |
| Battery drain target | <15% per hour | <20% per hour | N/A |

### PC (Minimum Spec / Recommended)

| Parameter | Minimum | Recommended |
|-----------|---------|-------------|
| Target FPS | 30 | 60 |
| Draw calls per frame | <2000 | <5000 |
| Triangle count per frame | <2M | <10M |
| Texture memory | <2GB VRAM | <4GB VRAM |
| RAM usage | <4GB | <8GB |
| Disk space | <5GB (indie), <20GB (AA) | Scalable |

### Console (Switch / PS5 / Xbox Series)

| Parameter | Switch | PS5 / Xbox Series X |
|-----------|--------|---------------------|
| Target FPS | 30 (docked), 30 (handheld) | 60 (performance), 30 (quality) |
| Draw calls per frame | <1000 | <5000 |
| Triangle count per frame | <500K | <10M |
| Texture memory | <2GB shared | <8GB |
| Disk space | <8GB (digital limit awareness) | <50GB |

## 2. 3D Model Specifications

### Polygon Budgets By Asset Type

| Asset Type | Mobile | PC (Indie) | PC (AA/AAA) |
|-----------|--------|-----------|------------|
| Player character | 3K-8K tris | 10K-25K tris | 30K-100K tris |
| NPC/enemy (common) | 1.5K-5K tris | 5K-15K tris | 15K-50K tris |
| Boss / hero enemy | 5K-12K tris | 15K-30K tris | 50K-150K tris |
| Environment prop (small) | 100-500 tris | 300-2K tris | 1K-5K tris |
| Environment prop (large) | 500-2K tris | 2K-8K tris | 5K-20K tris |
| Vehicle | 2K-6K tris | 8K-20K tris | 20K-80K tris |
| Weapon/handheld | 500-2K tris | 2K-5K tris | 5K-15K tris |

### LOD (Level of Detail) Requirements

| LOD Level | Distance | Triangle Reduction | Usage |
|-----------|----------|-------------------|-------|
| LOD0 | Close-up / hero | 100% (full detail) | Player character, inspected objects |
| LOD1 | Medium distance | 50-60% of LOD0 | Most gameplay view distance |
| LOD2 | Far distance | 25-30% of LOD0 | Background, distant objects |
| LOD3 / Billboard | Very far | <10% or sprite | Environment filler |

Rule: Any model visible at varying distances MUST have at least 2 LOD levels. Player character needs 3.

## 3. Texture Specifications

### Texture Size Limits

| Asset Type | Mobile | PC (Indie) | PC (AA/AAA) |
|-----------|--------|-----------|------------|
| Character (diffuse/albedo) | 512x512 - 1024x1024 | 1024x1024 - 2048x2048 | 2048x2048 - 4096x4096 |
| Character (normal map) | 512x512 | 1024x1024 | 2048x2048 |
| Environment tile/trim | 256x256 - 512x512 | 512x512 - 1024x1024 | 1024x1024 - 2048x2048 |
| UI elements | 64x64 - 256x256 | 128x128 - 512x512 | 256x256 - 1024x1024 |
| Skybox (per face) | 512x512 | 1024x1024 | 2048x2048 - 4096x4096 |
| VFX texture | 128x128 - 256x256 | 256x256 - 512x512 | 512x512 - 1024x1024 |

### Texture Compression Formats

| Platform | Recommended Format | Notes |
|----------|-------------------|-------|
| iOS | ASTC (4x4 to 8x8) | Best quality-to-size ratio on Apple GPUs |
| Android (modern) | ASTC (4x4 to 8x8) | Requires OpenGL ES 3.2+ or Vulkan |
| Android (legacy) | ETC2 | Fallback for older devices, lower quality |
| PC | BC7 (quality) / BC1 (size) | DXT5 for alpha, BC5 for normal maps |
| Switch | ASTC or BC7 | Engine-dependent |
| PS5 / Xbox | BC7 | GNF (PS5 native) for first-party optimization |

### Texture Atlas Rules

- Sprite atlases: max 2048x2048 (mobile), 4096x4096 (PC/console)
- Pack sprites by usage context (UI atlas, character atlas, VFX atlas) — not all-in-one
- Leave 1-2px padding between sprites to prevent bleeding
- Power-of-two dimensions required for mipmapping

## 4. Material and Shader Specifications

### PBR Material Workflow

Standard PBR texture set per material:

| Map | Required | Format | Notes |
|-----|----------|--------|-------|
| Albedo / Base Color | Yes | RGB (no lighting info baked in) | sRGB color space |
| Normal Map | Yes (3D), Optional (2D) | RGB (tangent space) | Linear color space |
| Metallic / Roughness | Yes (3D) | Grayscale or packed channels | Linear, often packed: R=Metallic, G=Roughness |
| Ambient Occlusion | Recommended | Grayscale | Can pack into unused channel |
| Emissive | Optional | RGB | For glowing effects only |
| Height / Displacement | Optional | Grayscale | For parallax or tessellation |

### Shader Complexity Budget

| Shader Type | Mobile Instructions | PC Instructions | Usage |
|-------------|-------------------|----------------|-------|
| Unlit / UI | <10 | <20 | HUD, particles, simple sprites |
| Standard PBR | <30 | <100 | Most game objects |
| Complex (subsurface, water) | <50 | <200 | Hero materials, special effects |
| Post-processing (per pass) | <20 | <50 | Bloom, color grading, SSAO |

Rule: On mobile, total unique shader variants should stay under 30-50 to minimize compilation hitches.

## 5. Animation Specifications

### Animation Budget Per Character Type

| Character Type | Mobile | PC (Indie) | PC (AA/AAA) |
|---------------|--------|-----------|------------|
| Player (action game) | 20-40 clips | 30-80 clips | 80-200+ clips |
| Player (RPG/adventure) | 15-30 clips | 25-50 clips | 50-120 clips |
| Common enemy | 8-15 clips | 12-25 clips | 20-50 clips |
| Boss | 15-25 clips | 20-40 clips | 40-80 clips |
| NPC (non-combat) | 5-10 clips | 8-15 clips | 15-30 clips |

### Minimum Animation State List (Action Character)

| State | Required Clips | Notes |
|-------|---------------|-------|
| Idle | 1-2 (idle, idle_break) | Idle_break triggers after 5-10s |
| Locomotion | 3-6 (walk, run, sprint, strafe L/R, walk_back) | Blend tree recommended |
| Jump | 3 (jump_start, jump_loop, jump_land) | Separate light and heavy landing optional |
| Attack (light) | 2-4 (combo chain) | Must define cancel windows |
| Attack (heavy) | 1-2 | Longer startup, more damage |
| Dodge/roll | 1-2 (forward, directional) | i-frame window defined in design |
| Hit react | 2-3 (light_hit, heavy_hit, knockdown) | Impact feel critical |
| Death | 1-2 | Ragdoll transition optional |
| Block/parry | 2 (block_start, block_hit) | If applicable |
| Interact | 1-2 (pickup, use) | Context-dependent |

### Skeletal Rig Specifications

| Rig Type | Bone Count (Mobile) | Bone Count (PC) | Notes |
|----------|-------------------|-----------------|-------|
| Humanoid | 25-40 bones | 40-80 bones | Fingers optional on mobile |
| Quadruped | 20-35 bones | 35-60 bones | Tail and ear bones add expressiveness |
| Simple creature | 10-20 bones | 15-30 bones | Blob enemies, slimes |
| Facial rig | 15-25 bones or blendshapes | 30-60 blendshapes | Full face animation is expensive |

## 6. Audio Technical Specifications

| Parameter | Mobile | PC / Console |
|-----------|--------|-------------|
| BGM format | OGG Vorbis (128-192 kbps) | OGG Vorbis (192-320 kbps) or WAV |
| SFX format | WAV (16-bit, 44.1kHz) | WAV (16-bit or 24-bit, 44.1-48kHz) |
| Simultaneous voices | 16-32 | 64-128 |
| Total audio memory | <64MB (mobile), <128MB (mid) | <256MB |
| Compression | ADPCM for frequent SFX, Vorbis for music | PCM for critical SFX, Vorbis for music |

## 7. UI Technical Specifications

| Parameter | Mobile | PC | Console |
|-----------|--------|-----|---------|
| Minimum touch target | 44x44 pt (iOS), 48x48 dp (Android) | 24x24 px | 48x48 px equivalent |
| Base UI resolution | 1080x1920 (portrait) or 1920x1080 (landscape) | 1920x1080 | 1920x1080 |
| UI scale support | Must handle 16:9, 18:9, 19.5:9, 21:9 | 16:9, 21:9, windowed arbitrary | 16:9 |
| Font minimum size | 14pt body, 11pt caption | 12pt body, 9pt caption | 24pt body, 18pt caption (couch distance) |
| Safe area | Respect iOS safe area insets, Android notch | Full screen usable | Title-safe: 90% of screen |

## 8. Outsourcing Art Spec Template

When generating art specs for outsourcing or team handoff, include:

```
ASSET: [Name]
TYPE: [Character / Environment / Prop / VFX / UI]
TARGET PLATFORM: [Mobile / PC / Console / Cross-platform]
ENGINE: [Unity / Unreal / Godot / Custom]

POLYGON BUDGET: [X tris max, LOD levels required]
TEXTURE BUDGET: [Albedo: Xpx, Normal: Xpx, format: ASTC/BC7/etc.]
MATERIAL: [PBR standard / Unlit / Custom shader needed]
RIG: [Bone count, IK requirements]
ANIMATION: [Clip list with frame ranges]

REFERENCE: [Style bible link, concept art, reference images]
NAMING CONVENTION: [prefix_assetname_variant_LOD.ext]
DELIVERY FORMAT: [FBX / glTF / PNG / engine-native]
```

---
**EXPERT DIRECTIVE:** When generating any art specification, asset list, or outsourcing brief, you MUST apply the platform-appropriate limits from this document. Art that looks great but runs at 15 FPS is a failure. Always verify: polygon count, texture size, draw call impact, and memory footprint against the target platform before finalizing specs.
